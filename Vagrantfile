# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version.
# Don't change unless you know what you're doing!i
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "chef/ubuntu-14.04"

  # Create a forwarded port mapping which allows access to a specific port
  # Rails server port
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  # Postgresql server port
  # Uncomment this in case that you want to access postgresql from you host machine
  config.vm.network "forwarded_port", guest: 5432, host: 5433
  # Kalibro processor port
  # Uncomment this in case that you want to access kalibro processor from you host machine
  config.vm.network "forwarded_port", guest: 8082, host: 8092
  # Kalibro configuration port
  # Uncomment this in case that you want to access kalibro configurations from you host machine
  config.vm.network "forwarded_port", guest: 8083, host: 8093

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Configuration for cooking with chef
  config.vm.provision :chef_solo do |chef|
    # Cooking :)
    chef.cookbooks_path = ["cookbooks"]
    chef.add_recipe "mezuro"
    chef.add_recipe "mezuro::analizo"
    chef.add_recipe "mezuro::kalibro_processor"
    chef.add_recipe "mezuro::kalibro_configurations"
    chef.add_recipe "mezuro::prezento"

    # Setting up Ruby 2.2.2, Bundle and PostgreSQL
    chef.json = {
      postgresql: {
        password: { postgres: "" },
        config: { "listen_addresses" => '*' }
      },
      :rvm => {
         'rubies' => ["2.2.2"],
         'default_ruby' => "2.2.2",
         :vagrant => { :system_chef_solo => "/opt/chef/bin/chef-solo" }
      }
    }
  end

  # Configuration for kalibro processo and configuration
  # config.vm.provision :shell, path: "script/install-kp-kc.sh"

end
