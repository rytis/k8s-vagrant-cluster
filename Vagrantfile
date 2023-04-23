# -*- mode: ruby -*-
# vi: set ft=ruby :

OS_IMAGE = "generic/fedora37"
CONTROL_PLANE_HOSTS = 1
WORKER_HOSTS = 2

Vagrant.configure("2") do |config|

  cp_hosts = []
  wrk_hosts = []

  (1..CONTROL_PLANE_HOSTS).each do |i|
    cp_hosts.push("k8s-c#{i}")
  end

  (1..WORKER_HOSTS).each do |i|
    wrk_hosts.push("k8s-w#{i}")
  end

  config.vm.synced_folder ".", "/vagrant"
  config.vm.network "public_network", bridge: "en0: Ethernet"
  config.vm.box = "generic/fedora37"

  (1..(CONTROL_PLANE_HOSTS+WORKER_HOSTS)).each do |i|

    if i <= CONTROL_PLANE_HOSTS
      hostname = "k8s-c#{i}"
      mem = "2048"
    else
      hostname = "k8s-w#{i-CONTROL_PLANE_HOSTS}"
      mem = "4096"
    end

    config.vm.provision "shell",
      run: "always",
      inline: "ip route del default via 10.0.2.2 || true"

    config.vm.define hostname do |subconf|

      subconf.vm.provider "virtualbox" do |vb|
        vb.memory = mem
      end

      if i == (CONTROL_PLANE_HOSTS+WORKER_HOSTS)
        subconf.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.playbook = "ansible/playbook.yml"
          ansible.groups = {
            "control" => cp_hosts,
            "worker" => wrk_hosts
          }
          ansible.extra_vars = {
            _v_control_primary: "k8s-c1"
          }
        end
      end
    end
  end
end
