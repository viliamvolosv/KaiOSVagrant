# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.require_version ">= 2.1"
Vagrant.configure("2") do |config|
  config.vm.box = "bstoots/xubuntu-16.04-desktop-amd64"
  config.vm.network "forwarded_port",
                guest: 6000,
                host: 6000,
                host_ip: "127.0.0.1",
                auto_correct: true

  config.vm.provider "virtualbox" do |vb|
    vb.name = "WebOS_Dev_VM2"
    vb.memory = "4096"
    vb.cpus = 2
	vb.gui = true
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
    vb.customize ['modifyvm', :id, '--clipboard', 'bidirectional']
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
    vb.customize ['modifyvm', :id, '--draganddrop', 'bidirectional']
  end

#  config.vm.synced_folder "./",
#                "/vagrant",
#                type: "rsync",
#                rsync__auto: true,
#                rsync__exclude: [".git/", ".idea/", "node_modules", ".vagrant"],
#                create: true

  config.vm.provision :shell, privileged: false, inline: <<-SHELL
        echo "---------------------------Start Setup----------------------------------"
        log="webos_dev_log"

        wget http://ftp.us.debian.org/debian/pool/main/m/make-dfsg/make_3.81-8.2_amd64.deb
        sudo dpkg -i make_3.81-8.2_amd64.deb
        sudo apt-mark hold make

        sudo apt-get update
        sudo apt-get -yqq install rsync
        sudo apt install --no-install-recommends autoconf2.13 bison bzip2 ccache curl flex gawk gcc g++ g++-multilib git lib32ncurses5-dev lib32z1-dev libgconf2-dev zlib1g:amd64 zlib1g-dev:amd64 zlib1g:i386 zlib1g-dev:i386 libgl1-mesa-dev libx11-dev make zip lzop libxml2-utils openjdk-8-jdk nodejs unzip python
        sudo dpkg --add-architecture amd64
        sudo apt install android-tools-adb android-tools-fastboot
        echo "---------------------------Setup for KaiOS sim----------------------------------"
        wget --output-document=kaiossim.tar.gz https://developer.kaiostech.com/simulator/linux
        mkdir ~/KaiOSSimulator
        tar xf kaiossim.tar.gz -C ~/KaiOSSimulator/
        cd ~/KaiOSSimulator/b2g
        #./b2g-bin -profile ./gaia/profile -start-debugger-server 6000
  SHELL
end
