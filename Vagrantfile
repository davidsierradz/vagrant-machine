# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "~/code/", "/home/vagrant/code/"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
  apt-get update
  apt-get install -y apache2
  apt-get install -y php5 libapache2-mod-php5 php5-mcrypt
  SHELL

  ############################################################
  # Oh My ZSH Install section

  # Install git and zsh prerequisites 
  config.vm.provision :shell, 
  inline: "apt-get -y install git"
  config.vm.provision :shell, 
  inline: "apt-get -y install zsh"

  # Clone Oh My Zsh from the git repo
  config.vm.provision :shell, privileged: false,
  inline: "git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh"
  
  # Copy in the default .zshrc config file
  config.vm.provision :shell, privileged: false,
  inline: "git clone https://github.com/davidsierradz/dotfiles.git"
  config.vm.provision "shell", privileged: false,
  inline: "cd ~/dotfiles && git checkout vagrant"
  config.vm.provision :shell, privileged: false,
  inline: "cp ~/dotfiles/zsh/.zshrc ~/.zshrc"
  # Change the vagrant user's shell to use zsh
  config.vm.provision :shell,
  inline: "chsh -s /bin/zsh vagrant"

  ############################################################

############################################################
  # Vim Install section

  # Install git and zsh prerequisites   
  config.vm.provision :shell, 
  inline: "apt-get -y install vim"
  config.vm.provision :shell, privileged: false,
  inline: "mkdir -p .vim"
  config.vm.provision :shell, privileged: false,
  inline: "mkdir -p .vim/bundle"
  config.vm.provision :shell, privileged: false,
  inline: "git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim"
  config.vm.provision :shell, privileged: false,
  inline: "cp ~/dotfiles/vim/.vimrc ~/.vimrc"
  
  # Instalar los plugines de Vim, no he encontrado la forma de que
  # la provision de Vagrant lo ejecute sin errores.
  #config.vm.provision :shell, privileged: false,
  #inline: "ex +PluginInstall || :"

  ############################################################

  #config.vm.network "private_network", ip: "192.168.10.192"
  config.vm.network "forwarded_port", guest: 80, host: 1234
end
