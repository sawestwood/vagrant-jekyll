VERSION  = 2
BOX      = 'ubuntu/xenial64'
HOSTNAME = ENV['VAGRANT_JEKYLL_HOSTNAME']

Vagrant.configure(VERSION) do |config|
	config.vm.box = BOX
	config.vm.hostname = HOSTNAME
	config.vm.network "forwarded_port", guest: 4000, host: 4000	
	config.vm.provider "virtualbox" do |vb|
		vb.customize ["modifyvm", :id, "--memory", 4096]
		vb.name = HOSTNAME
	end
	config.vm.synced_folder ENV['RUBY_SRC'], "/home/vagrant/src/"

	config.vm.provision :shell, :inline => "gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB"
	config.vm.provision :shell, :inline => "curl -sSL https://get.rvm.io | bash -s stable"
	config.vm.provision :shell, :inline => "source /usr/local/rvm/scripts/rvm"
	config.vm.provision :shell, :inline => "rvm requirements"
	config.vm.provision :shell, :inline => "bash -l -c 'rvm use --default --install 2.5.0'"

	config.vm.provision :shell, :inline => "gem install bundler"
	config.vm.provision :shell, :inline => "gem install jekyll"
end
