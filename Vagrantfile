# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_USER = 'vagrant'
ENV["LC_ALL"] = "en_US.UTF-8"

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  
  config.vm.box = "centos/7"

  config.vm.hostname = 'vagrant-' + ENV['USER']
  
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  config.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", auto_correct: true
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  # meal-planner port
  config.vm.network "forwarded_port", guest: 8443, host: 8443

  config.vm.network "private_network", ip: "192.168.200.20"

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "share", "/home/#{VAGRANT_USER}/share", create: true
  config.vm.synced_folder "#{ENV['HOME']}/gitrepo", "/home/#{VAGRANT_USER}/gitrepo", create: true

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true
  
    # Customize the amount of memory on the VM:
    vb.memory = 6144
    vb.cpus = 4

    # Make guest VM to use host's DNS resolver
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
