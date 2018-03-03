# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/alpine36"
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider "virtualbox" do |vb|
    vb.name = 'Alpine1'
    vb.cpus = 1
    vb.memory = 1024
  end
  config.vm.provision "shell", inline: <<-SHELL
    echo http://dl-3.alpinelinux.org/alpine/edge/main >> /etc/apk/repositories
    echo http://dl-3.alpinelinux.org/alpine/edge/community >> /etc/apk/repositories
    apk update
    apk add docker
    rc-update add docker boot
    service docker start
    sleep 2
    docker run -td -p 3000:3000 sendwithus/battlesnake-server
  SHELL

end
