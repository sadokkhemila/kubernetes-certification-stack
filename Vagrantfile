# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "master" do |master|
    master.vm.box = "geerlingguy/centos7"
    master.vm.network "private_network", type: "static", ip: "192.168.99.10"
    master.vm.hostname = "master"
    master.vm.provider "virtualbox" do |v|
      v.name = "masterd"
      v.memory = 2048
      v.cpus = 2
    end
    master.vm.provision :shell do |shell|
      shell.path = "install_kubernetes.sh"
      shell.args = ["master", "192.168.99.10"]
    end
  end
  workers=1
  ram_worker=2048
  cpu_worker=2
  (1..workers).each do |i|
    config.vm.define "worker#{i}" do |worker|
      worker.vm.box = "geerlingguy/centos7"
      worker.vm.network "private_network", type: "static", ip: "192.168.99.1#{i}"
      worker.vm.hostname = "worker#{i}"
      worker.vm.provider "virtualbox" do |v|
        v.name = "workerd#{i}"
        v.memory = ram_worker
        v.cpus = cpu_worker
      end
      worker.vm.provision :shell do |shell|
        shell.path = "install_kubernetes.sh"
        shell.args = ["node", "192.168.99.10"]
      end
    end
  end
end

