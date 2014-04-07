# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.require_version ">= 1.5.0"

if !Vagrant.has_plugin?('vagrant-omnibus')
  puts "Please install the vagrant-omnibus plugin"
  puts "You can install it like this: vagrant plugin install vagrant-omnibus"
  exit
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "saucy64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/saucy/current/saucy-server-cloudimg-amd64-vagrant-disk1.box"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 9200, host: 9200

  # Change this if you know what you're doing.
  # config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.synced_folder "./data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024"]
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  config.vm.provision :shell, :inline => "apt-get update && apt-get upgrade -y && apt-get install -y build-essential vim git curl"

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #

  config.omnibus.chef_version = :latest

  config.vm.provision "chef_solo" do |chef|
    chef.cookbooks_path = "./.chef/cookbooks"
    # chef.data_bags_path = "./.chef/data_bags"

    chef.add_recipe "java"
    chef.add_recipe "elasticsearch"

    chef.json = {
      "java" => {
        "install_flavor" => "oracle",
        "jdk_version" => "8",
        "oracle" => {
          "accept_oracle_download_terms" => true
        }
      },

      "elasticsearch" => {
        "name" => "elasticsearch_test_vagrant_wooo",
        "network.bind_host" => "0.0.0.0"
      }
    }
  end

end
