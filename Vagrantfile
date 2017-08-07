# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.ssh.username = "vagrant"
  config.ssh.forward_agent = true
  config.vm.provision :shell, :path => "vagrant_setup.sh", :privileged => false
  # Sync a folder between the host and all guests.
  # Uncomment this line (and adjust as you like)
  #config.vm.synced_folder "~/code", "/code"

  config.vm.define "pwn", primary: true do |u64|
    u64.vm.provider "virtualbox" do |vb, override|
      override.vm.box ="geerlingguy/ubuntu1604"
      override.vm.network "private_network", ip: "10.10.10.10"
      
      vb.name = "pwn"
      vb.memory = "2048"
      vb.gui = false
    end
    u64.vm.provider "libvirt" do |lv, override|
      override.vm.box = "algebro/ubuntu1604"
      override.vm.network "private_network", ip: "10.10.10.10"      

      lv.memory = "2048"
      lv.graphics_type = "none"
    end
  end
end
