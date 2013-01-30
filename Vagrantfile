# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|

  config.vm.box = "precise64"

  config.vm.forward_port  80, 4567
  config.vm.host_name = "wordpress.ms-local.com"
  config.vm.customize [ "modifyvm", :id, "--memory", 256]
  
  # ensure the latest packages
  config.vm.provision :chef_solo do |chef|  

    # This path will be expanded relative to the project directory
    chef.cookbooks_path = "cookbooks" 
    chef.roles_path = "roles"

    chef.add_recipe "apt"
    chef.add_role "base"
    chef.add_recipe "mysql::server"
    chef.add_recipe "wordpress"


    chef.json.merge!({
      :mysql => {
        :server_debian_password => "secure_password",
        :server_root_password => "secure_password",
        :server_repl_password => "secure_password"
      },

      # Virtual-Host
      :wordpress_hostname => "wordpress.42foo.com",
      "build_essential" => {
        "compiletime" => true
      }
    })
  
  end
end
