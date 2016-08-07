# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url = "http://files.vagrantup.com/trusty64.box"
  config.vm.hostname = "ubuntu-graphite"

  cpu = ENV['VAGRANT_CPU'] || 2
  ram = ENV['VAGRANT_MEMORY'] || 1024

  config.vm.provider :virtualbox do |vm, override|
    vm.customize ["modifyvm", :id, "--memory", ram]
    vm.customize ["modifyvm", :id, "--cpus", cpu]
    vm.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    #vm.gui = true # for debug
  end
  
  config.vm.network :forwarded_port, guest: 80, host: 1080
  config.vm.network :forwarded_port, guest: 8082, host: 1082
  config.vm.network :forwarded_port, guest: 8125, host: 1125
  
  if Vagrant.has_plugin?("vagrant-hostsupdater")
    # https://github.com/cogitatio/vagrant-hostsupdater
    config.hostsupdater.aliases = ['stats.webfolks.be']
  end

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = 'vvv'
    ansible.playbook = "playbook.yml"
  end
end
