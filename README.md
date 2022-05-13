# printserver ansible setup

an ansible server setup for a simple, single host print server so I dont have to do it again hopefully

```
.
├── ansible.cfg
├── docs
│   └── NOTES.md
├── hosts
├── roles
│   └── printserver
│       ├── defaults
│       │   └── main.yml
│       ├── handlers
│       │   └── main.yml
│       ├── tasks
│       │   └── main.yml
│       └── templates
│           ├── cupsd.conf.j2
│           └── smb.conf.j2
├── site.yaml
└── vars
    └── default.yml
```

## usage

configure `hosts` to have the addresses and entries for 1 or more print servers

1 should be enough though surely for goodness

copy ssh key to the target(s) as normal and run `ansible all -m ping` to check connectivity

run the playbook :

```
ansible-playbook --limit printserver -e "ansible_sudo_pass=${ansible_sudo}" site.yaml
```

This uses jinja2 templates ( see the templates directory under the printserver role ) to configure 2 configuration files for cups and samba - these may need changing to suit your requirements where 'defaults/main.yml' contains some simple variables that could be altered by setting at the command line or by injecting new values to suit

Once run, the printserver will be running and on port 631 a web interface will permit the final setup of your printer. HP drivers are installed by default as I have HP printers but others would need to be added if required.

