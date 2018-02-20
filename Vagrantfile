# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_VERSION  = 2
BOX = 'ubuntu/xenial64'
HOSTNAME = ENV['VAGRANT_JEKYLL_HOSTNAME']

$script = <<SCRIPT
  sudo apt-get -qy update
  sudo apt-get -qy install curl ruby-dev build-essential dh-autoreconf libssl-dev zlib1g-dev libxml2 libxml2-dev libxslt1-dev libreadline-dev

  git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
  echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
  echo 'eval "$(rbenv init -)"'               >> ~/.bashrc
  source ~/.bashrc

  git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
  sudo -H -u vagrant bash -i -c 'rbenv install 2.5.0'
  sudo -H -u vagrant bash -i -c 'rbenv rehash'
  sudo -H -u vagrant bash -i -c 'rbenv global 2.5.0'
  sudo -H -u vagrant bash -i -c 'gem install bundler --no-ri --no-rdoc'
  sudo -H -u vagrant bash -i -c 'gem install jekyll --no-ri --no-rdoc'
  sudo -H -u vagrant bash -i -c 'rbenv rehash'
SCRIPT

Vagrant.configure(VAGRANTFILE_VERSION) do |config|
	config.vm.box = BOX
	config.vm.hostname = HOSTNAME
	config.vm.network "forwarded_port", guest: 4000, host: 4000, host_ip: "127.0.0.1"
	config.vm.provider "virtualbox" do |vb|
		vb.customize ["modifyvm", :id, "--memory", 4096]
		vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    	vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
		vb.name = HOSTNAME
	end

	config.vm.synced_folder ENV['RUBY_SRC'], "/home/vagrant/src/"

	config.vm.provision :shell, privileged: false, inline: $script
end
