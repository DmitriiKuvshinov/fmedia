# -*- mode: ruby -*-
# vi: set ft=ruby :
home = ENV['HOME']
MACHINES = {
  :server => {
        :box_name => "wordpress-server",
	:disks => {
		:sata1 => {
			:dfile => home + '/VirtualBox VMs/disks/sata1.vdi',
			:size => 5000,
			:port => 1
		        }
                }
  }
}
Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.provider "virtualbox"
  config.vm.network "forwarded_port", host_ip: "127.0.0.1", guets_ip: "10.0.2.15", guest: 80, host: 2280, auto_correct: true
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.become = "true"
    ansible.tags = "deployhost"
  end

  config.vm.provider "virtualbox" do |v|
	  v.memory = 2048
    
  end

  config.vm.define "wordpress" do |wordpress|
    wordpress.vm.hostname = "wordpress"
    
  end
  
end
