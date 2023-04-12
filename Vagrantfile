# -*- mode: ruby -*-
# vi: set ft=ruby :

OS_IMAGE = "generic/fedora37"
CONTROL_PLANE_HOSTS = 1
WORKER_HOSTS = 2

Vagrant.configure("2") do |config|

  (1..CONTROL_PLANE_HOSTS).each do |i|
    config.vm.define "k8s-c#{i}" do |subconf|
      subconf.vm.synced_folder ".", "/vagrant"
      subconf.vm.network "public_network", bridge: "en0: Ethernet"
      subconf.vm.box = "generic/fedora37"
      subconf.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
      end
      subconf.vm.provision :ansible do |ansible|
        # ansible.verbose = "vvv"
        ansible.playbook = "ansible/control.yml"
        ansible.extra_vars = {
          _v_hostname: "k8s-c#{i}"
        }
      end
    end
  end

  # (1..WORKER_HOSTS).each do |i|
  #   config.vm.define "k8s-w#{i}" do |subconf|
  #     subconf.vm.network "public_network", bridge: "en0: Ethernet"
  #     subconf.vm.box = "generic/fedora37"
  #     subconf.vm.provider "virtualbox" do |vb|
  #       vb.memory = "4096"
  #     end
  #   end
  # end

end
