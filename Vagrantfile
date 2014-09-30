# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.hostname = "guest"
  config.vm.box = "opscode-centos-6.5"

  config.vm.define "dbmaster" do |dbmaster|
    dbmaster.vm.hostname = "dbmaster"
    dbmaster.vm.network :private_network, ip: "192.168.33.10"
  end

  config.vm.define "dbslave" do |dbslave|
    dbslave.vm.hostname = "dbslave"
    dbslave.vm.network :private_network, ip: "192.168.33.11"
  end

  config.omnibus.chef_version = :latest
  config.vm.provision "chef_solo" do |chef|
     chef.cookbooks_path = ["./cookbooks", "./site-cookbooks"]
  #   chef.roles_path = "../my-recipes/roles"
  #   chef.data_bags_path = "../my-recipes/data_bags"
     chef.add_recipe "yum-epel"
     chef.add_recipe "nginx"
  #   chef.add_recipe "php-env::php55"
     chef.add_recipe "ruby-env"
     chef.add_recipe "nodejs"
     chef.add_recipe "mysql"
  #   chef.add_role "web"
  #
  #   # You may also specify custom JSON attributes:
     chef.json = {
       nginx: {
         env: ["php", "ruby"]
       },
       mysql: {
         server_root_password: 'rootpass'
       }
     }
  end
end
