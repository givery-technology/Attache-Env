# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu1404"
  config.vm.hostname = "Attache"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.synced_folder "../data", "/home/vagrant/data", type: "nfs"
  config.vm.provider :virtualbox do |vb|
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/home/vagrant/data", "1"]
    vb.customize ["modifyvm", :id, "--memory", 1024]
  end
end
