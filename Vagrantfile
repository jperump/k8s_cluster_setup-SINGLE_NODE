# -*- mode: ruby -*-
# vi: set ft=ruby :
# Defining an IP for the guest vm
controlplane_IP = "192.168.47.1"

Vagrant.configure("2") do |config|
  # Defining a VM image 
  config.vm.box = "ubuntu/bionic64"

  # Disable automatic box update checking.
  config.vm.box_check_update = false

  # Configuring a sync folder to copy the ansible playbook to guest VM
  config.vm.synced_folder "Ansible_Playbooks", "/opt/ansible"


  # Provision controlplane node
  config.vm.define "controlplane" do |node|
    node.vm.provider "virtualbox" do |vb|
        vb.name = "controlplane"
        vb.memory = 2048
        vb.cpus = 2
    end
    node.vm.hostname = "controlplane"
    node.vm.network :private_network, ip: controlplane_IP
    node.vm.network "forwarded_port", guest: 22, host: "#{2711}"

    node.vm.provision "ip_setup", :type => "shell", :path => "ip_setup.sh" do |input|
      input.args = ["enp0s8"]
    end
  # Using ansible-playbook to provision k8s cluster
    config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "/opt/ansible/k8s_setup.yml"
 
    end
  end
end
