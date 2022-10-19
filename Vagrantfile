# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  workers=1
  ram_worker=2048
  cpu_worker=2
  (1..workers).each do |i|
    config.vm.define "worker#{i}" do |worker|
      worker.vm.box = "geerlingguy/centos7"
      worker.vm.network "private_network", type: "static", ip: "192.168.99.1#{i}"
      worker.vm.hostname = "worker#{i}"
      worker.vm.provider "virtualbox" do |v|
        v.name = "MachineWP"
        v.memory = ram_worker
        v.cpus = cpu_worker
      end
      worker.vm.provision :shell do |shell|
        shell.path = "install_jenkins.sh"
        shell.args = ["worker", workers]
      end
    end
  end
end
