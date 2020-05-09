# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # kubMaster
  config.vm.define "kubMaster" do |kubMaster|
    kubMaster.vm.box = "centos/7"
    kubMaster.vm.hostname = "kubMaster"
    kubMaster.vm.box_url = "centos/7"
    kubMaster.vm.provision = "docker"

    kubMaster.vm.network :private_network, ip: "192.168.1.30"

    kubMaster.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2072]
      v.customize ["modifyvm", :id, "--name", "kubMaster"]
      v.customize ["modifyvm", :id, "--cpus", "2"]
    end
  end

  # kubNode
  config.vm.define "kubNode" do |kubNode|
    kubNode.vm.box = "centos/7"
    kubNode.vm.hostname = "kubNode"
    kubNode.vm.box_url = "centos/7"
    kubMaster.vm.provision = "docker"

    kubNode.vm.network :private_network, ip: "192.168.1.31"

    kubNode.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2072]
      v.customize ["modifyvm", :id, "--name", "kubNode"]
      v.customize ["modifyvm", :id, "--cpus", "2"]
    end
  end
end
