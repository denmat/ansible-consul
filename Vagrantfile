# -*- mode: ruby -*-
# vi: set ft=ruby :
require 'yaml'
def details
  @details || YAML.load_file([File.dirname(__FILE__), '/', 'group_vars/vagrant.yml'].join)
end

def extras(n)
  if n < 4 
  {
    consul_qorum: 3,
    consul_server: true,
  #  join: "172.16.10.#{rand(1..3)}"
    join: ['172.16.10.1..3', '172.16.10.2', '172.16.10.3']
  }
  else
  { join: [ "172.16.10.#{rand(1..3)}" ] }
  end
end

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'ubuntu/trusty64'

  config.ssh.private_key_path = "~/.ssh/vagrant.key"

5.times do |n|
  n = n + 1
  config.vm.define "consul#{n}" do |v|
    v.vm.hostname
    v.vm.network "private_network", ip: "172.16.10.#{n}"
    v.vm.provision 'shell',
      inline: "dpkg -l ansible || bash -c 'sudo apt-get install -y software-properties-common && sudo apt-add-repository -y ppa:ansible/ansible && sudo aptitude update && sudo aptitude install ansible python-apt -y' && hostname consul#{n}"
    v.vm.provision "ansible" do |ansible|
      ansible.playbook = "plays/local.yml"
      ansible.verbose = 'v'
      ansible.sudo = true
      ansible.extra_vars = extras(n)
      end
    end
  end
end
