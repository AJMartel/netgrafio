# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

$hostname = "netgrafio"
$ip = "192.168.33.90"

$init = <<SCRIPT
sudo apt-get -y update
sudo apt-get -y install git python-pip python3-pip tshark traceroute nmap
sudo pip3 install virtualenv
sudo pip3 install -r /vagrant/env/requirements.pip
hostname
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 1
    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end
  
  config.vm.define $hostname do |v|
    v.vm.box = "ubuntu1404"
    v.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-i386-vagrant-disk1.box"
    v.vm.hostname = $hostname
    v.vm.network "private_network", ip: $ip
    v.ssh.forward_agent = true
    v.vm.provision :shell, :inline => $init
  end
  
end
