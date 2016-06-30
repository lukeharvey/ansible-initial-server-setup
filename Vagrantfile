# Defines our Vagrant environment
#
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.provider :virtualbox do |virtualbox|
    virtualbox.customize ["modifyvm", :id, "--memory", 1024]
    virtualbox.customize ["modifyvm", :id, "--cpus", 1]
    virtualbox.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    virtualbox.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.define "test" do |machine|
    machine.vm.hostname = "test"
    machine.vm.network :private_network, ip: "192.168.2.2"
    machine.ssh.insert_key = false
  end
end
