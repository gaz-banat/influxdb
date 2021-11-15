# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "Centos/7"

  BOX_COUNT = 1
  (1..BOX_COUNT).each do |machine_id|
	  
    config.vm.define "influx#{machine_id}" do |machine|
	    
      machine.vm.hostname = "influx#{machine_id}"
      machine.vm.network "private_network", type: "dhcp"
      machine.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 1
      end

      machine.vm.provision "ansible" do |ansible|
        ansible.limit = 'all'
        ansible.playbook = "influxdb-playbook.yaml"
        ansible.sudo = true
        ansible.host_key_checking = false
        ansible.extra_vars = {
          is_vagrant: true,
        }
      end
      
    end

  end

end
