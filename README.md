OTOBO development environment
=============================

Here you find the Vagrant file and Ansible playbooks needed for set up a complete OTOBO development environment with three guest VMs: a MySQL database VM, a OTOBO production application server VM and a OTOBO development application server VM.

Instructions
============

Install Vagrant, Vagrant libvirt plugin and Ansible on your host machine. You may need to install aditional Ansible modules.

Run `vagrant up`.

Run `vagrant status` and verify the status of each VM.

Run `vagrant ssh <guest_name>`.

After provision all the guests, you need to complete OTOBO installation using the OTOBO web installer.

I suggest create two databases, otobo-pd for the production VM, and otobo-dv for the development VM.


