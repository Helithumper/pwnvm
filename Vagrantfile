# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.ssh.username = "vagrant"
  config.ssh.forward_agent = true
  
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
  end

  name = "VIRTPWN"
  memory = "4096"
  shared_directory = "~/Documents/"

  config.vm.define "VIRTPWN", primary: true do |u64|
    u64.vm.network "private_network", ip: "10.10.10.10"
    u64.vm.provider "virtualbox" do |vb, override|
      override.vm.box ="geerlingguy/ubuntu1804"

      ## For Syncing of CTF Directory between host and VM
      override.vm.synced_folder shared_directory, "/host", owner: "vagrant", group: "vagrant"

      vb.name = name
      vb.memory = memory
      vb.gui = false
      vb.cpus = 4
    end
    u64.vm.provider "libvirt" do |lv, override|
      override.vm.box = "algebro/ubuntu1604"
      lv.memory = memory
      lv.graphics_type = "none"
    end
  end
end
