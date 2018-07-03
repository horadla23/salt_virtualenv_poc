Vagrant.configure("2") do |config|
   os = "centos/7"
   net_ip = "192.168.50"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "salt.yml"
#    ansible.verbose  = true
  end

  config.vm.define :master, primary: true do |master_config|
    master_config.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.cpus = 1
        vb.name = "master"
    end
    master_config.vm.box = "#{os}"
    master_config.vm.hostname = 'saltmaster'
    master_config.vm.network "private_network", ip: "#{net_ip}.10"
  end

  [
    ["minion1",    "#{net_ip}.11",    "1024",    os, "2221" ],
    ["minion2",    "#{net_ip}.12",    "1024",    os, "2222" ],
  ].each do |vmname,ip,mem,os,ssh_port|
    config.vm.define "#{vmname}" do |minion_config|
      minion_config.vm.provider "virtualbox" do |vb|
          vb.memory = "#{mem}"
          vb.cpus = 1
          vb.name = "#{vmname}"
      end
      minion_config.vm.box = "#{os}"
      minion_config.vm.hostname = "#{vmname}"
      minion_config.vm.network "private_network", ip: "#{ip}"
    end
  end
end
