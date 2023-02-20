# PXE Server with Ansible and Vagrant
## Prerequisites
Install Ansible, Vagrant, and Virtualbox
* Note: This runs best in Linux and MacOS but Vagrant and Ansible can be installed in WSL2 as well (see notes below).

## Ansible
This repository contains all the required files to configure a PXE server using Ansible. This server will serve up Rocky Linux 9 in it's current configuration. All the listed IP addresses will need to be changed to match your network.

## Vagrant
I used Vagrant for quick and easy testing of my configurations. The listed Vagrantfile will deploy a Rocky linux VM in VirtualBox and provision it with playbook.yml

After testing in Vagrant, I used the same Ansible playbooks to configure a laptop as my PXE server.

## DHCP
Change the IP range and default gateway IP in the config file to match your network. The dnsmasq.conf is configured as proxy DHCP to avoid conflict with your existing DHCP server. Your current DHCP server (or router) will provide IP addresses, and this dnsmasq will point to the location of the PXE boot file.

## Using WSL2
Virtualbox will need to be installed in Windows (not WSL) but Vagrant and Ansible should be installed in WSL2.


## FTP
Using ansible's copy module to move the iso files from the mount point to the /var/ftp folder does not allow the directories to be visible in FileZilla. To get around this, I used thed shell module and then used cp to move the files. This solved the issue.