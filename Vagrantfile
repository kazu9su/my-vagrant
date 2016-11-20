# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box      = "ubuntu/trusty64"

  config.vm.hostname = "personal-vagrant"
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.synced_folder "sync/", "/srv/sync", create: true

  config.vm.provision "shell", inline: <<-CMD
    sudo apt-get update \\
    && sudo add-apt-repository -y ppa:brightbox/ruby-ng \\
    && sudo apt-get install -y ruby2.1 git \\
    && sudo gem i bundler --no-rdoc --no-ri \\
    && sudo apt-get install nfs-common portmap
  CMD

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end

  config.vm.synced_folder "./src", "/opt/src", :nfs => true, :create => true
end
