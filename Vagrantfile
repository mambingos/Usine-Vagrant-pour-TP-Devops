# -*- mode: ruby -*-
# vi: set ft=ruby :

$script_inject_pk =<<-'SCRIPT'
cat /vagrant/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys
SCRIPT

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |configuration|
# General Vagrant VM configuration.
  configuration.ssh.insert_key = false

# Dev machine
(1..2).each do |i|
  configuration.vm.define "dev#{i}" do |app|
    app.vm.hostname = "dev#{i}"
    app.vm.box = "ubuntu/focal64"
    app.vm.network :private_network, ip: "192.168.60.10#{i}"
    app.vm.provision "shell", inline: $script_inject_pk
    end
  end

(3..4).each do |i|
  configuration.vm.define "dev#{i}" do |app|
    app.vm.hostname = "dev#{i}"
    app.vm.box = "centos/7"
    app.vm.network :private_network, ip: "192.168.60.10#{i}"
    app.vm.provision "shell", inline: $script_inject_pk
    end
  end


# Ansible machine
  configuration.vm.define "ansible" do |app|
    app.vm.hostname = "ansible"
    app.vm.box = "centos/7"
    app.vm.network :private_network, ip: "192.168.60.110"
    app.vm.provision "file", source: "./id_rsa", destination: "/home/vagrant/.ssh/"
    end
  

# Jenkins machines
  configuration.vm.define "jenkins1" do |app|
    app.vm.hostname = "jenkins1"
    app.vm.box = "centos/7"
    app.vm.network :private_network, ip: "192.168.60.121"
    app.vm.provision "shell", inline: $script_inject_pk
    app.vm.provider :virtualbox do |v|
      v.memory = 8192
      end
  end

  configuration.vm.define "jenkins2" do |app|
    app.vm.hostname = "jenkins2"
    app.vm.box = "ubuntu/focal64"
    app.vm.network :private_network, ip: "192.168.60.122"
    app.vm.provision "shell", inline: $script_inject_pk
    app.vm.provider :virtualbox do |v|
      v.memory = 8192
      end
  end

end

