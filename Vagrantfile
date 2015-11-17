# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com//precise64.box"
  config.vm.network :private_network, ip: "192.168.33.10"
  config.ssh.insert_key = false
  config.vm.define "base" do |base|
  end

  config.vm.provider :virtualbox do |v|
    v.name = "docker.dev"
    v.memory = 1024
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # Enable provisioning with Ansible.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/main.yml"
    ansible.inventory_path = "hosts"
    ansible.limit = "all"
    ansible.verbose = "vv"
  end

end
