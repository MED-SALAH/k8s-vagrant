# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # kubmaster
  config.vm.define "kubmaster" do |kubmaster|
    kubmaster.vm.box = "centos/7"
    kubmaster.vm.hostname = "kubmaster"
    kubmaster.vm.box_url = "centos/7"
    kubmaster.vm.provision "docker"

    kubmaster.vm.network :private_network, ip: "192.168.1.30"

    kubmaster.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2072]
      v.customize ["modifyvm", :id, "--name", "kubmaster"]
      v.customize ["modifyvm", :id, "--cpus", "2"]
    end
  end

  # kubnode
  config.vm.define "kubnode" do |kubnode|
    kubnode.vm.box = "centos/7"
    kubnode.vm.hostname = "kubnode"
    kubnode.vm.box_url = "centos/7"
    kubnode.vm.provision "docker"

    kubnode.vm.network :private_network, ip: "192.168.1.31"

    kubnode.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2072]
      v.customize ["modifyvm", :id, "--name", "kubnode"]
      v.customize ["modifyvm", :id, "--cpus", "2"]
    end
  end
end
