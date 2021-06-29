# -*- mode: ruby -*-
# vi: set ft=ruby :



ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'


Vagrant.configure("2") do |config|
  ##### DEFINE VM #####
  config.vm.define "os-01" do |config|
    config.vm.hostname = "os-01.fq.dn"
    config.vm.box = "centos/8"
    config.vm.box_check_update = false
    config.vm.network "private_network", ip: "192.168.18.9"
    config.vm.provider :libvirt do |v|
      v.memory = 8192
      v.cpus = 8
      v.nested = true
      v.cpu_mode = "host-passthrough"
    end
    config.vm.provision "shell", inline: <<-SHELL
              dnf update -y
              dnf config-manager --enable powertools
              dnf install -y centos-release-openstack-ussuri
              dnf update -y
              dnf install -y openstack-packstack
              packstack --allinone
          SHELL
  end
end
