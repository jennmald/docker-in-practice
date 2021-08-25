Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"
  config.vm.box_check_update = true

  config.vm.network "forwarded_port", guest: 8001, host: 8001, host_ip: "127.0.0.1"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    # vb.memory = "4096"
    # vb.cpus = 4
  end

  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true

  config.vm.provision "shell", inline: <<-SHELL
    # https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04
    apt update
    apt full-upgrade
    apt install -y python3-pip
    # install X11 for matplotlib
    apt install -y xserver-xorg-core x11-utils
    # install docker
    apt install apt-transport-https ca-certificates curl software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
    apt update
    apt install -y docker-ce
    # add the vagrant account to the docker group
    # this way the vagrant account can run docker without sudo
    usermod -aG docker vagrant

  SHELL
  # ssh into the VM
  #   $ vagrant ssh

end
