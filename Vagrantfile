# -*- mode: ruby -*-
# vi: set ft=ruby :

# BOX = "hashicorp/precise64"
# BOX = "boxesio/wheezy64-ansible"
# BOX = "wheezy-vmware"
BOX = "geerlingguy/ubuntu1404"
RAM = "512"
CPUs = "1"

Vagrant.configure(2) do |config|
  config.vm.box = BOX
  config.ssh.insert_key = false

  #config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provider "vmware_fusion" do |v|
    v.gui = "true"
    v.name = "lamppp"
    v.memory = RAM
    v.cpus = CPUs
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.define :varnish do |varnish_config|
    varnish_config.vm.hostname = "varnish.dev"
    varnish_config.vm.network :private_network, ip: "192.168.55.11"
  end

  config.vm.define :web1 do |web1_config|
    web1_config.vm.hostname = "web1.dev"
    web1_config.vm.network :private_network, ip: "192.168.55.22"
  end

  config.vm.define :web2 do |web2_config|
    web2_config.vm.hostname = "web2.dev"
    web2_config.vm.network :private_network, ip: "192.168.55.33"
  end

  config.vm.define :db1 do |db1_config|
    db1_config.vm.hostname = "db1.dev"
    db1_config.vm.network :private_network, ip: "192.168.55.44"
  end

  config.vm.define :db2 do |db2_config|
    db2_config.vm.hostname = "db2.dev"
    db2_config.vm.network :private_network, ip: "192.168.55.55"
  end

   config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    #ansible.inventory_path = "inventories/vagrant/inventory"
    ansible.sudo = "true"
    ansible.verbose = "vv"
    ansible.limit = "all"
    ansible.extra_vars = {
      ansible_ssh_user: 'vagrant',
      ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
    }
  end

end
