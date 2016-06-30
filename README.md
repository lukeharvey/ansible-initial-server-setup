# Ansible Playbook for Initial Server Setup with Ubuntu 14.04

An [Ansible](http://docs.ansible.com/) playbook which runs a series of configuration steps to increase the security and usability of a new Ubuntu 14.04 server, in order to provide a solid foundation for subsequent actions.

It borrows heavily from the work of: [Bryan Kennedy](https://plusbryan.com/my-first-5-minutes-on-a-server-or-essential-security-for-linux-servers), [Ryan Eschinger](http://ryaneschinger.com/blog/securing-a-server-with-ansible/),  [Ashley Rich](https://github.com/A5hleyRich/wordpress-ansible), and [Digital Ocean](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04)

It will perform the following:
* Create a new "super user" with root privileges and public key authentication
* Implement several SSH hardening techniques
* Configure a basic firewall
* Configure the timezone and enable time synchronization
* Modify the hostname and hosts file
* Enable unattended upgrades
* Install Fail2Ban

Optional extras:
* Install New Relic Server monitoring
* Install customised shell with Zsh and oh-my-zsh

## Requirements

* [Ansible](http://docs.ansible.com/ansible/intro_installation.html) installed locally on your machine
* Root SSH access to a new Ubuntu 14.04 VPS

## Configuration

Clone the repo

```
$ git clone https://github.com/lukeharvey/ansible-initial-server-setup.git
```

Modify the variables in **_vars/main.yml_** according to your needs:

**user:** the username for your new "super user"

**password:** a [hashed](http://docs.ansible.com/ansible/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module) sudo password

**public_key:** the local path to your public SSH key

**fqdn:** your chosen [FQDN](https://kb.iu.edu/d/aiuv)

**hostname:** your chosen hostname

**timezone:** the most appropriate [timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) for your server

**ssh_port:** your chosen SSH port

**enable_newrelic:** change to `no` to disable installation of New Relic Server monitor, which requires a [New Relic license key](https://docs.newrelic.com/docs/accounts-partnerships/accounts/account-setup/license-key)

**newrelic_license_key:** your [New Relic license key](https://docs.newrelic.com/docs/accounts-partnerships/accounts/account-setup/license-key)

**enable_custom_shell:** change to `no` to disable installation of customised shell with Zsh and oh-my-zsh

## Testing

A Vagrantfile is provided which allows the playbook to be tested locally.

You will need Vagrant and Virtualbox installed, and you should uncomment the following lines in **_ansible.cfg_** to makes things work nicely.
```
# private_key_file = ~/.vagrant.d/insecure_private_key
# host_key_checking = False
```
Then run `$ vagrant up` to generate your virtual machine.

And then run the playbook:

`$ ansible-playbook test_server_setup.yml`

## Production

Add your server's IP address to the **_hosts_** file

```
[production]
# e.g 192.168.1.1
# or host.example.com
```

Then run the playbook:

`$ ansible-playbook initial_server_setup.yml --ask-pass`
