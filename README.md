DOCKER-LATEST
=========

Ansible role for latest docker-ce and docker-compose desired version. Also docker and docker-compose python modules
will be installed. Tested on:
- Ubuntu 14.04 Trusty
- Ubuntu 16.04 Xenial

Requirements
------------

Installed OS:
 - Ubuntu 14.04 Trusty
 - Ubuntu 16.04 Xenial

 Role Variables
 --------------

 - DOCKER_COMPOSE_VER: 1.18.0 # Desired docker-compose version
 - DOCKER_COMPOSE_FILE: /usr/local/bin/docker-compose # Docker-compose binary location

Example Playbook
----------------

To use this role:

  - create folder (in user $HOME folder in example below) and install role from ansible-galaxy

```bash
cd ~/
mkdir docker-latest
cd docker-latest
ansible-galaxy install winmasta.docker-latest --roles-path .
```

  - create file `hosts`, containing hostname(s) or IP address(es) of host(s), where you want to deploy docker-latest

```bash
echo "ENTER HOSTNAME OR IP" > hosts
```

  - create file `ansible.cfg` in current folder

```bash
cat > ansible.cfg << EOF
[defaults]
remote_user = root
host_key_checking = False
EOF
```

  - create playbook in current folder `main.yml` with content

```bash
cat > main.yml << EOF
---
- hosts: all
  gather_facts: no

  pre_tasks:

  - name: Install required packages
    raw: sudo apt-get update -y && sudo apt-get -y install python-simplejson python-pip
    changed_when: False

  - setup:

  roles:
    - winmasta.docker-latest
EOF
```

  - execute playbook `main.yml`

```bash
ansible-playbook -i hosts main.yml
```

License
-------

MIT
