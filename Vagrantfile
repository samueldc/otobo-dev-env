# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # https://github.com/vagrant-libvirt/vagrant-libvirt
  config.vagrant.plugins = "vagrant-libvirt"

  config.vm.provider :libvirt do |lv|
    lv.driver = "kvm"
    lv.cpus = "2"
    lv.memory = "1024"
  end

  # https://docs.ansible.com/ansible/latest/user_guide/index.html
  
  # Provision OTOBO production vm
  config.vm.define "otobo-pd", primary: true do |pd|
    pd.vm.box = "generic/ubuntu2004"
    pd.vm.network "private_network", ip: "10.0.0.11"
    pd.vm.network "forwarded_port", guest: 80, host: 8081
    pd.vm.hostname = "otobo-pd.localhost"
    # pd.vm.synced_folder "./", "/opt/otobo"
    pd.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.otobo-pd.yml"
      ansible.host_vars = {
        "otobo-pd" => {"ansible_python_interpreter" => "/usr/bin/python3"}
      }
      ansible.verbose = "-vvv"
    end
  end  
  
  # Provision OTOBO development vm
  config.vm.define "otobo-dv", primary: true do |dv|
    dv.vm.box = "generic/ubuntu2004"
    dv.vm.network "private_network", ip: "10.0.0.12"
    dv.vm.network "forwarded_port", guest: 80, host: 8082
    dv.vm.hostname = "otobo-dv.localhost"
    # dv.vm.synced_folder "/home/samueldc/Projects/otobo/", "/opt/otobo"
    dv.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.otobo-dv.yml"
      ansible.host_vars = {
        "otobo-dv" => {"ansible_python_interpreter" => "/usr/bin/python3"}
      }
      ansible.verbose = "-vvv"
    end
  end  
  
  # Provision Znuny production vm
  config.vm.define "znuny-pd", primary: true do |dv|
    dv.vm.box = "generic/ubuntu2004"
    dv.vm.network "private_network", ip: "10.0.0.13"
    dv.vm.network "forwarded_port", guest: 80, host: 8083
    dv.vm.hostname = "znuny-pd.localhost"
    # dv.vm.synced_folder "/home/samueldc/Projects/otobo/", "/opt/otobo"
    dv.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.znuny-pd.yml"
      ansible.host_vars = {
        "znuny-dv" => {"ansible_python_interpreter" => "/usr/bin/python3"}
      }
      ansible.verbose = "-vvv"
    end
  end  
  
  # Provision OTOBO database vm
  config.vm.define "otobo-db" do |db|
    db.vm.box = "debian/buster64"
    db.vm.network "private_network", ip: "10.0.0.101"
    # db.vm.network "forwarded_port", guest: 3306, host: 3316, host_ip: "127.0.0.1"
    db.vm.hostname = "otobo-db.localhost"
    db.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.otobo-db.yml"
      ansible.host_vars = {
        "otobo-db" => {"ansible_python_interpreter" => "/usr/bin/python3"}
      }
      ansible.verbose = "-vvv"
    end
  end

end