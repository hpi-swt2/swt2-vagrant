# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  #config.vm.box = "ubuntu/trusty32"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", 2]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    vb.customize ["modifyvm", :id, "--hwvirtex", "on"]
  end

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks", "site-cookbooks"]

    chef.add_recipe "apt"
    chef.add_recipe "ruby_build"
    chef.add_recipe "ruby_rbenv::user"
    chef.add_recipe "vim"
    chef.add_recipe "postgresql::server"
    chef.add_recipe "postgresql::client"
    chef.add_recipe "postgresql::libpq"

    chef.json = {
      rbenv: {
        user_installs: [{
          user: 'vagrant',
          rubies: ["2.4.0"],
          global: "2.4.0",
          gems: {
            "2.4.0" => [
              { name: "bundler" }
            ]
          }
        }]
      },
      postgresql: {
        users: [
          {
            username: "postgres",
            password: "",
            superuser: true,
            createdb: true,
            login: true
          },
          {
            username: "vagrant",
            password: "",
            superuser: false,
            createdb: true,
            login: true
          },
        ],
       databases: [
          {
            name: "hpi_swt2_dev",
            owner: "vagrant",
            template: "template0",
            encoding: "UTF-8",
            locale: "en_US.UTF-8",
            extensions: "hstore"
          },
          {
            name: "hpi_swt2_test",
            owner: "vagrant",
            template: "template0",
            encoding: "UTF-8",
            locale: "en_US.UTF-8",
            extensions: "hstore"
          },
          {
            name: "hpi_swt2_production",
            owner: "vagrant",
            template: "template0",
            encoding: "UTF-8",
            locale: "en_US.UTF-8",
            extensions: "hstore"
          },

        ]
      },

    }
  end

end
