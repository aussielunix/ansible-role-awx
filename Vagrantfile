# -*- mode: ruby -*-
# vi: set ft=ruby :

boxes = [
  {
    :name => "controller-1.home.arpa",
    :hostname => "controller-1.home.arpa",
    :ports => [8052],
    :memory => 4096,
    :cpus => 2
  },
  {
    :name => "worker-1.home.arpa",
    :hostname => "worker-1.home.arpa",
    :ports => [],
    :memory => 2048,
    :cpus => 2
  },
  {
    :name => "worker-2.home.arpa",
    :hostname => "worker-2.home.arpa",
    :ports => [],
    :memory => 2048,
    :cpus => 2
  }
]

Vagrant.configure("2") do |config|
  config.ssh.connect_timeout = 30
  config.vm.box_check_update = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider :libvirt do |v|
    v.management_network_name = "default"
    v.management_network_keep = true
  end

  boxes.each_with_index do |box, index|
    config.vm.define box[:name] do |box_config|
      box_config.vm.hostname = box[:hostname]
      box_config.vm.box = "roboxes/centos9s"
      box_config.vm.network "private_network", type: "dhcp", :libvirt__domain_name => "home.arpa"
      box_config.vm.provider :libvirt do |v|
        v.memory = box[:memory]
        v.cpus = box[:cpus]
      end
      box[:ports].each do |port|
        box_config.vm.network "forwarded_port", guest: port, host: port, autocorrect: true
      end

      if index == boxes.size - 1
        box_config.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.playbook = "tests/vagrant/provision.yml"
          ansible.verbose = "-v"
          #ansible.verbose = false
          ansible.groups = {
            "controllers" => ["controller-1.home.arpa"],
            "workers" => [
              "worker-1.home.arpa",
              "worker-2.home.arpa"
            ]
          }
        end
      end
      box_config.vm.provision :shell, inline: "sudo firewall-cmd --add-port=8052/tcp --permanent"
      box_config.vm.provision :shell, inline: "sudo firewall-cmd --add-port=27199/tcp --permanent"
    end
  end
end

