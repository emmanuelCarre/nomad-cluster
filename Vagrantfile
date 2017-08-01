# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|

  config.vm.box = "centos/7"

  N = 5
  VAGRANT_VM_PROVIDER="libvirt"
  ANSIBLE_RAW_SSH_ARGS = []

  (1..N).each do |machine_id|
    ANSIBLE_RAW_SSH_ARGS << "-o IdentityFile=.vagrant/machines/machine#{machine_id}/#{VAGRANT_VM_PROVIDER}/private_key"
  end

  (1..N).each do |machine_id|
    config.vm.define "machine#{machine_id}" do |machine|

      machine.vm.hostname = "machine-#{machine_id}"
      machine.vm.network "private_network", ip: "192.168.77.#{20+machine_id}"

      if machine_id == N
        machine.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.playbook = "./resources/playbook.yml"
          ansible.inventory_path = "./resources/inventory"
          ansible.raw_ssh_args = ANSIBLE_RAW_SSH_ARGS
        end
      end

    end
  end

end
