# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
settings = YAML.load_file('Vagrantsettings.yaml')

$root = File.dirname(__FILE__)

Vagrant.configure(2) do |config|
  config.vm.box = settings["vm"]["box"]

  if Vagrant.has_plugin?("vagrant-timezone")
    config.timezone.value = settings["vm"]["timezone"]
  end

  # extra mounts
  # config.vm.synced_folder "/Users/admin/VagrantMachines/share", "/home/vagrant"
  # config.vm.synced_folder "./dotfiles", "/home/vagrant/dotfiles"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = settings["vm"]["gui"]

    vb.cpus = settings["vm"]["cpus"]
    vb.memory = settings["vm"]["memory"]
    # auto-NAT
    vb.customize [
      'modifyvm', :id,
      '--natdnshostresolver1', 'on',
      '--nic1', 'nat',
      '--cableconnected1', 'on'
    ]

    vb.customize [ "guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 1000 ]
    vb.customize [ "guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-interval", 10000 ]
    vb.customize [ "guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-min-adjust", 100 ]
  end

  config.vm.provision "shell", run: "always", inline: <<-SHELL
    apt-get update
  SHELL

  config.vm.provision "shell", path: "scripts/custom.sh"
  # config.vm.provision "shell", path: "scripts/dotfiles.sh", privileged: false
end
