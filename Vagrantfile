Vagrant.configure('2') do |config| # rubocop:disable Style/FrozenStringLiteralComment
  config.vm.box = 'ubuntu/focal64'
  config.vm.provision 'docker'
  config.vm.provision 'shell', path: './scripts/bootstrap.sh'

  config.vm.define 'vm1' do |vm1|
    vm1.vm.hostname = 'vm1'
    vm1.vm.network 'private_network', ip: '192.168.56.11'
    vm1.vm.hostname = 'vm1.tecknohjem.com'
    vm1.vm.provider 'virtualbox' do |v|
      v.memory = 2048
      v.name = 'vm1'
    end
    vm1.vm.provision 'shell', path: './scripts/setup_master.sh'
  end

  (2..3).each do |i|
    config.vm.define "vm#{i}" do |vm|
      vm.vm.hostname = "vm#{i}"
      vm.vm.network 'private_network', ip: "192.168.56.1#{i}"
      vm.vm.hostname = "vm#{i}.tecknohjem.com"
      vm.vm.provider 'virtualbox' do |v|
        v.memory = 2048
        v.name = "vm#{i}"
      end
      vm.vm.provision 'shell', path: './scripts/setup_worker.sh'
    end
  end
end
