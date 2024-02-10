# Basic Server Setup
This repository contains an Ansible playbook which is used to perform the basic setup tasks for my development and productions environments.

## Features
The playbook configures the provided servers based on their given groups to quickly provide a sane default starting point. This is achieved by using some roles which are provided by the community and configuring/customizing them to suit my needs.

**All Servers**
  * Configure sane defaults for SSH. (Disable root login, require key-based authentication, custom SSH port)
  * Setup fail2ban for SSH monitoring.
  * Setup a custom user with passworded sudo access.
  * Setup a basic iptables firewall configuration only allowing access to port 22.

**Group: docker_hosts**
  * Setup a basic docker installation incl. the docker-compose plugin.
  * Setup and add a customer user to the docker group.

**Group: webservers**
  * Setup additional firewall rules to allow access via HTTP & HTTPS.

## Role Variables
For a full list of the executed actions and available configurations please refer to the original repositories of the used roles.
  * [ansible-role-security](https://github.com/geerlingguy/ansible-role-security)
  * [ansible-role-docker](https://github.com/geerlingguy/ansible-role-docker)
  * [ansible-role-firewall](https://github.com/saiba-tenpura/ansible-role-firewall/tree/custom) - A slightly modified version of the Ansible firewall role originally written by Jeff Geerling. (The exact differences can be viewed [here](https://github.com/geerlingguy/ansible-role-firewall/compare/master...saiba-tenpura:ansible-role-firewall:custom).)

## Inventory Variables
A couple of additional variables are defined in the inventory group_vars to control multiple options of the executed roles.
```
main_ssh_port: 22
```

Defines the port through which SSH is accessible and adds it to the allowed TCP ports for the firewall role. (Corresponding role variables: security_ssh_port, firewall_allowed_tcp_ports)
```
main_system_user: main
```

Defines the user which is allowed to access the server via SSH, added as a sudoer and is assigned to the docker group. (Corresponding role variables: security_ssh_allowed_users, security_sudoers_passworded, docker_users)

## Installation
```
ansible-galaxy install -r roles/requirements.yml
```

## Setup Execution
```
ansible-playbook -i inventory/example/ main.yml
```

## Updating mailservers
```
ansible-playbook -i inventory/example/ mailwhales.yml
```

## License
MIT

## Author
This project was created in 2022 by Saiba Tenpura.
