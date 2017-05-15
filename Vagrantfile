# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "first8/f8forum-base"
    
  config.vm.define "web" do |web|
    web.vm.hostname = "web"
    web.vm.network "private_network", ip: "192.168.33.20"
    
    web.vm.provider :virtualbox do |vb|
      vb.name = "f8f_web"
    end
        
    web.vm.provision "ansible_local" do |ansible|
      ansible.playbook = 'bootstrap_web.yml'
      ansible.install_mode = 'pip'
      ansible.version = '2.2.2.0'
    end
  end
  
  config.vm.define "database" do |database|
    database.vm.hostname = "database"
    database.vm.network "private_network", ip: "192.168.33.30"
    
    database.vm.network "forwarded_port", guest: 5432, host: 2345
    
    database.vm.provider :virtualbox do |vb|
      vb.name = "f8f_database"
    end
    
    database.vm.provision "ansible_local" do |ansible|
      ansible.playbook = 'bootstrap_database.yml'
      ansible.install_mode = 'pip'
      ansible.version = '2.2.2.0'
    end
  end
	
  config.vm.define "controller" do |controller|
    controller.vm.hostname = "controller"
    controller.vm.network "private_network", ip: "192.168.33.10"
    
    controller.vm.provider :virtualbox do |vb|
      vb.name = "f8f_controller"
    end
    
    controller.vm.provision "ansible_local" do |ansible|
      ansible.playbook = 'bootstrap.yml'
      ansible.install_mode = 'pip'
      ansible.version = '2.2.2.0'
    end
  end


  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
 

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"


end
