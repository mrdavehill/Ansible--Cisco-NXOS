## Ansible--Cisco-NXOS

On this page:

group_vars/   -    NXOS Ansible variable

host_vars/    -    Host specific variables (ip addresses etc)

Vagrantfile   -    Instructions for Virtualbox to set up four NXOSv VMs

ansible.cfg   -    Ansible settings

inventory.yaml -   List of all four VMs with some host specific variables

main.yaml     -    For future use (advanced config using roles)

provisioner.yaml - Ansible playbook adding basic configuration to the VMs (ip addresses, hostnames, lldp and macs)
 
### Use Case Description

Create and provision a 'Bow-Tie' network using Vagrant, Ansible and Cisco NXOSv images

### How to test the software

git clone https://github.com/mrdavehill/Ansible--Cisco-NXOS.git

Download nxosv.9.2.3 image from Cisco.com

Install Virtualbox

Install and configure Vagrant

Install Ansible (min 2.9)

From the command line type:

$ vagrant up; vagrant up; vagrant up; vagrant up

$ vagrant provision

### Getting help

Hit me up if you have any issues.

### Author

This project was written and is maintained by the following Daves:

* Dave Hill <dave@davehill.org>
* https://www.linkedin.com/in/dave-hill-a5a3601b0/
