# Basic Server Setup
This repository contains an Ansible playbook which is used to perform the basic setup tasks for my development and productions environments.

## Features
The playbook configures the provided servers based on their given groups to quickly provide me with a sane default starting point. This is achieved by using

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
  * [ansible-role-firewall](https://github.com/saiba-tenpura/ansible-role-firewall/tree/custom) - A slightly modified version of the Ansible firewall role originally written by Jeff Geerling. ([Exact differences](https://github.com/geerlingguy/ansible-role-firewall/compare/master...saiba-tenpura:ansible-role-firewall:custom))

## Installation
```
ansible-galaxy install -r roles/requirements.yml
```

## Execution
```
ansible-playbook -i inventory/development/ main.yml
```

## License
MIT

## Author
This project was created in 2022 by Saiba Tenpura.