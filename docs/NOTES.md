taken from :

https://www.linuxbabe.com/ubuntu/set-up-cups-print-server-ubuntu-bonjour-ipp-samba-airprint

# when all done, the CUPS service should be available at

# http://[print servers ip address]:631/


# here we go ...

sudo apt install cups

# Then start CUPS.

sudo systemctl start cups

# Enable auto-start at boot time.

sudo systemctl enable cups

# Check its status:

systemctl status cups

# sudo nano /etc/cups/cupsd.conf

###   diff /etc/cups/cupsd.conf.orig /etc/cups/cupsd.conf
###   18c18,19
###   < Listen localhost:631
###   ---
###   > #Listen localhost:631
###   > Port 631
###   22c23
###   < Browsing On
###   ---
###   > Browsing Off
###   33a35
###   >   Allow @LOCAL
###   38a41
###   >   Allow @LOCAL
###
###

sudo systemctl restart cups

# sudo adduser your_username lpadmin

sudo apt install hplip

# I also recommend installing the printer-driver-gutenprint package, which provides CUPS drivers for Canon, Epson, HP and compatible printers.

sudo apt install printer-driver-gutenprint

# skipping apple bonjour setup

sudo apt install samba samba-common-bin

# start these two services, issue the following commands:
sudo systemctl start smbd
sudo systemctl start nmbd

# To check if Samba service is running, issue the following commands.
systemctl status smbd
systemctl status nmbd

# sudo nano /etc/samba/smb.conf


###   diff /etc/samba/smb.conf.orig /etc/samba/smb.conf
###   25a26,28
###   > rpc_server:spoolss = external
###   > rpc_daemon:spoolssd = fork
###   >
###   215c218
###   <    browseable = no
###   ---
###   >    browseable = yes
###   218c221
###   <    guest ok = no
###   ---
###   >    guest ok = yes
###






sudo systemctl restart smbd nmbd