# -*- mode: ruby -*-
# vi: set ft=ruby :

#########################
$CPU = 4
$MEMORY = 8192
$CPUEXECUTIONCAP = 50
$IP = "192.168.0.2"
$BASEOS = "centos/7"
$SSH=2223
#########################

Vagrant.configure("2") do |config|
  config.vm.box = $BASEOS

  config.vm.provider "virtualbox" do |v|
    v.memory = $MEMORY
    v.cpus = $CPU
    v.customize ["modifyvm", :id, "--cpuexecutioncap", $CPUEXECUTIONCAP]
  end
  
  config.vm.network "private_network", ip: $IP
  config.vm.network "forwarded_port", guest: 22, host: $SSH, id: 'ssh'

  config.vm.provision "ansible" do |ansible|
    ansible.galaxy_role_file = "requirements.yml"
    ansible.playbook = "playbook.yml"
  end
  
end
