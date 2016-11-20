# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box_check_update = false
  
  ui = Vagrant::UI::Colored.new

  base_box = "ubuntu/trusty64"
  
  machines = {
    :manager1 => {:ip => '192.168.56.10'},
    :worker1 => {:ip => '192.168.56.21'},
    :worker2 => {:ip => '192.168.56.22'},
  }

  machines.each do |machine_name, machine_details|
    config.vm.define machine_name do |machine_config|
      machine_config.vm.box = base_box
      ui.info("Handling vm with hostname [#{machine_name.to_s}] and IP [#{machine_details[:ip]}]")
      machine_config.vm.network :private_network, ip: "#{machine_details[:ip]}"
      machine_config.vm.hostname = machine_name.to_s
      machine_config.vm.provider :virtualbox do |vb|
        vb.name = machine_name.to_s
      end
      machine_config.vm.provision :ansible_local do |ansible|
        ansible.playbook 		= "docker.yml"
	ansible.verbose = true
	ansible.provisioning_path	= "/vagrant/ansible"
      end
    end
  end

end
