# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|


  config.vm.define "db" do |db|
    db.vm.box = "ubuntu2210"
    db.vm.hostname = "Ubuntu-2210"
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    wget https://ftp.postgresql.org/pub/source/v8.4.1/postgresql-8.4.1.tar.gz
    tar -xvf postgresql-8.4.1.tar.gz
    cd postgresql-8.4.1
#     libreadline-dev
    sudo apt-get install zlib1g zlib1g-dev build-essential -y
    ./configure --without-readline
    gmake
    sudo -i
    cd /home/vagrant/postgresql-8.4.1/
    gmake install clean
    sudo useradd postgres -p postgres -U -m
    mkdir /usr/local/pgsql/data
    chown postgres /usr/local/pgsql/data
    su - postgres
#     https://www.postgresql.org/docs/8.4/install-procedure.html
    /usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data
    /usr/local/pgsql/bin/postgres -D /usr/local/pgsql/data >logfile 2>&1 &
    /usr/local/pgsql/bin/createdb test
    /usr/local/pgsql/bin/psql test
  SHELL

#   config.vm.provision "shell", inline: <<-SHELL
#     apt-get update
# #     apt-get install apache2 -y
#
# #     wget -q -O nibiru.sh https://api.nodes.guru/nibiru.sh && chmod +x nibiru.sh && sudo /bin/bash nibiru.sh
# #     source $HOME/.bash_profile
#   SHELL

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end
end
