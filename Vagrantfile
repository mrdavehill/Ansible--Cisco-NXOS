# -*- mode: ruby -*-
# vi: set ft=ruby :

# Bowtie / Mesh Topology
# +---------+e3          e3+---------+
# | spine01 |--------------| spine02 |
# +---------+              +---------+
#   |e1    \ e2          e1 /    e2|
#   |        \            /        |
#   |          \        /          |
#   |            \    /            |
#   |              \/              |
#   |             /  \             |
#   |           /      \           |
#   |         /          \         |
#   |e1     / e2        e1 \     e2|
# +---------+              +---------+
# | leaf03  |--------------| leaf04  |
# +---------+e3          e3+---------+

##################################################################################
#                                                                                #
# shrink RAM to 5GB, sort the console connection and switch-to-switch networking #
#                                                                                #
##################################################################################

Vagrant.configure(2) do |config|
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "5120"
    vb.customize ['modifyvm', :id, '--uart1', '0x3F8', 4, '--uartmode1', 'disconnected']
    vb.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
    vb.customize ["modifyvm", :id, "--nicpromisc3", "allow-all"]
    vb.customize ["modifyvm", :id, "--nicpromisc4", "allow-all"]
  config.vm.boot_timeout = 5
  end

##################################################################################
#                                                                                #
# ansible provisioner                                                            #
#                                                                                #
##################################################################################

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "./provisioner.yaml"
    ansible.inventory_path = "./inventory.yaml"
    ansible.extra_vars = "./group_vars/nxos.yaml"
  end

##################################################################################
#                                                                                #
# spine01                                                                        #
#                                                                                #
##################################################################################

  config.vm.define 'spine01' do |spine01|
    spine01.vm.box = 'nxosv.9.2.3'
    spine01.vm.network 'private_network',
                       virtualbox__intnet: 's01l03',
                       ip: '169.254.1.11', auto_config: false
    spine01.vm.network 'private_network',
                       virtualbox__intnet: 's01l04',
                       ip: '169.254.1.11', auto_config: false
    spine01.vm.network 'private_network',
                       virtualbox__intnet: 's01s02',
                       ip: '169.254.1.11', auto_config: false
    spine01.vm.network :forwarded_port, guest: 22, host: 3122, id: 'ssh', auto_correct: true
  end

##################################################################################
#                                                                                #
# spine02                                                                        #
#                                                                                #
##################################################################################

  config.vm.define 'spine02' do |spine02|
    spine02.vm.box = 'nxosv.9.2.3'
    spine02.vm.network 'private_network',
                       virtualbox__intnet: 's02l03',
                       ip: '169.254.1.11', auto_config: false
    spine02.vm.network 'private_network',
                       virtualbox__intnet: 's02l04',
                       ip: '169.254.1.11', auto_config: false
    spine02.vm.network 'private_network',
                       virtualbox__intnet: 's01s02',
                       ip: '169.254.1.11', auto_config: false
    spine02.vm.network :forwarded_port, guest: 22, host: 3222, id: 'ssh', auto_correct: true
  end

##################################################################################
#                                                                                #
# leaf03                                                                         #
#                                                                                #
##################################################################################

  config.vm.define 'leaf03' do |leaf03|
    leaf03.vm.box = 'nxosv.9.2.3'
    leaf03.vm.network 'private_network',
                       virtualbox__intnet: 's01l03',
                       ip: '169.254.1.11', auto_config: false
    leaf03.vm.network 'private_network',
                       virtualbox__intnet: 's02l03',
                       ip: '169.254.1.11', auto_config: false
    leaf03.vm.network 'private_network',
                       virtualbox__intnet: 'l03l04',
                       ip: '169.254.1.11', auto_config: false
    leaf03.vm.network :forwarded_port, guest: 22, host: 3322, id: 'ssh', auto_correct: true
  end

##################################################################################
#                                                                                #
# leaf04                                                                         #
#                                                                                #
##################################################################################

  config.vm.define 'leaf04' do |leaf04|
    leaf04.vm.box = 'nxosv.9.2.3'
    leaf04.vm.network 'private_network',
                       virtualbox__intnet: 's01l04',
                       ip: '169.254.1.11', auto_config: false
    leaf04.vm.network 'private_network',
                       virtualbox__intnet: 's02l04',
                       ip: '169.254.1.11', auto_config: false
    leaf04.vm.network 'private_network',
                       virtualbox__intnet: 'l03l04',
                       ip: '169.254.1.11', auto_config: false
    leaf04.vm.network :forwarded_port, guest: 22, host: 3422, id: 'ssh', auto_correct: true
  end
end

