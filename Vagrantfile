# -*- mode: ruby -*-

# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!

VAGRANTFILE_API_VERSION = "2"
RAM_ASSIGNED = "512"

nodes = {
  'node1' => {
    'ip' => '192.168.78.2',
  },
  'node2' => {
    'ip' => '192.168.78.3',
  },
}

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "nrel/CentOS-6.5-x86_64"
  config.vm.boot_timeout = 600
  (1..2).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.provider :virtualbox do |vb|
          vb.customize ["modifyvm", :id, "--memory", RAM_ASSIGNED]
          vb.customize ["modifyvm", :id, "--cpus", "1"]
      end
      node.vm.network "private_network", ip: nodes["node#{i}"]['ip']
      node.vm.hostname = "node#{i}"
      node.vm.provision :ansible do |ansible|
        ansible.playbook = "playbook.yml"
        ansible.verbose = "yes"
      end
    end
  end
end
