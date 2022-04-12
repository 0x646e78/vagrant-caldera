# -*- mode: ruby -*-
# vi: set ft=ruby :
#

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2004"
  # config.vm.box_check_update = false

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "172.30.1.2"
  
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y python3-pip
    snap install go --classic
    git clone https://github.com/mitre/caldera.git --recursive --branch 2.8.1
    cd caldera
    pip3 install -r requirements.txt
    chown vagrant:vagrant -R ../
  SHELL
  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    cd caldera
    cp -a conf/default.yml conf/local.yml
    sed -i 's,0.0.0.0:,172.30.1.2:,g' conf/local.yml #listening IP
    sed -i "s,REPLACE_WITH_RANDOM_VALUE,$(openssl rand -base64 32)," conf/local.yml #salt value
    python3 server.py -E local &
  SHELL
end

