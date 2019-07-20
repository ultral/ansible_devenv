# -*- mode: ruby -*-
# vi: set ft=ruby :

# set default values
no_proxy   = ENV['no_proxy']
http_proxy = ENV['http_proxy']

puts "Use http_proxy: #{http_proxy}"
puts "Use no_proxy  : #{no_proxy}"

# *****************************************************************************#
Vagrant.configure('2') do |config|
  # configure vagrant-proxyconf plugin
  unless http_proxy.nil?
    config.proxy.enabled  = true
    config.proxy.http     = http_proxy
    config.proxy.https    = http_proxy
    config.proxy.no_proxy = no_proxy
  end

  config.ssh.insert_key = false

  config.vm.synced_folder '../',
                          '/vagrant',
                          mount_options: ['dmode=775,fmode=644']
  config.vm.box = 'bento/centos-7.6'

  config.vm.box_download_insecure = true
  config.vm.provision 'ansible_local' do |ansible|
    ansible.playbook = '/vagrant/ansible-devenv/provision_me.yml'
    ansible.config_file = '/vagrant/ansible-devenv/ansible.cfg'
    ansible.verbose = 'v'
  end

  config.vm.provider 'virtualbox' do |v|
    v.memory = 2048
  end
end
