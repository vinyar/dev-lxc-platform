# -*- mode: ruby -*-
# # vi: set ft=ruby :

# The following Vagrant plugins are required
# vagrant-berkshelf
# vagrant-omnibus
# vagrant-persistent-storage
#   until further notice Marc Paradise's fork of vagrant-persistent-storage must be used
#   to install it please follow these instructions

#   git clone https://github.com/marcparadise/vagrant-persistent-storage.git
#   cd vagrant-persistent-storage
#   gem build vagrant-persistent-storage.gemspec
#   vagrant plugin install vagrant-persistent-storage-0.0.5.gem

Vagrant.configure("2") do |config|
  config.vm.box = "opscode-ubuntu-13.10"
  config.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_ubuntu-13.10_chef-provisionerless.box"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--cpus", "4"]
    vb.customize ["modifyvm", :id, "--memory", "4096"]
  end

  config.persistent_storage.enabled = true
  config.persistent_storage.manage = false
  config.persistent_storage.format = false
  config.persistent_storage.size = 40 * 1024
  config.persistent_storage.location = File.expand_path("~/VirtualBox VMs/dev-lxc.vdi")

  config.vm.synced_folder "../downloads", "/downloads"

  config.berkshelf.enabled = true

  config.vm.network :private_network, ip: "33.33.34.13"

  config.omnibus.chef_version = :latest

  config.vm.provision :chef_solo do |chef|
    # chef.log_level = :debug
    chef.add_recipe "dev-lxc"
  end
end
