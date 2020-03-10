# -*- mode: ruby -*-
# vi: set ft=ruby :

#########################
$CPU = 2
$MEMORY = 4096
$CPUEXECUTIONCAP = 50
$IP = "192.168.0.5"
$BASEOS = "centos/7"
$SSH=2225
#########################

Vagrant.configure("2") do |config|
  config.vm.box = $BASEOS

  config.vm.provider "virtualbox" do |v|
    v.memory = $MEMORY
    v.cpus = $CPU
    v.customize ["modifyvm", :id, "--cpuexecutioncap", $CPUEXECUTIONCAP]
  end
  
  config.vm.provider "hyperv" do |v|
    v.memory = $MEMORY
    v.cpus = $CPU
  end

  config.vm.synced_folder ".", "/vagrant"

  config.vm.network "private_network", ip: $IP
  config.vm.network "forwarded_port", guest: 22, host: $SSH, id: 'ssh'

  config.vm.provision "ansible_local" do |ansible|
    ansible.galaxy_role_file = "/vagrant/requirements.yml"
    ansible.playbook = "/vagrant/playbook.yml"
  end
  
end
