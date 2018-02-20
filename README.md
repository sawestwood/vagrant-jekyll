# vagrant-jekyll

This creates a [Vagrant](https://www.vagrantup.com) VM for use im Jekyll development. The VM is based upon [Ubuntu Xenial 64-bit 16.04](https://app.vagrantup.com/ubuntu/boxes/xenial64) and:
* Installs [rbenv](https://github.com/rbenv/rbenv/)
* Sets up rbenv to use Ruby 2.5.0
* Installs Bundler and Jekyll gems

Two environment variables are required
* VAGRANT_JEKYLL_HOSTNAME - a name that Vagrant will associate with the new VM
* RUBY_SRC - the local source folder in which source resides inside the host OS

To use this file:
* Install [Vagrant](https://www.vagrantup.com)
* Install [VirtualBox](https://www.virtualbox.org/) 
* Clone this repository
* In the folder where the file resides run `vagrant up` to create a new VM
* To connect to the VM, use `vagrant ssh` 