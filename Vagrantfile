Vagrant.configure('2') do |config| # rubocop:disable Style/FrozenStringLiteralComment
  config.vm.box = 'ubuntu/focal64'

  config.vm.define 'vm1' do |vm1|
    vm1.vm.hostname = 'vm1'
    vm1.vm.network 'private_network', ip: '192.168.56.11'
    vm1.vm.provision 'docker'
    vm1.vm.provision 'shell', inline: [
      '/bin/sh installing_k8s.sh',
      '/bin/sh kubeadm init'
    ].join(';')
  end

  (2..3).each do |i|
    config.vm.define "vm#{i}" do |vm|
      vm.vm.hostname = "vm#{i}"
      vm.vm.network 'private_network', ip: "192.168.56.1#{i}"
      vm.vm.provision 'docker'
      vm.vm.provision 'shell', inline: [
        '/bin/sh installing_k8s.sh',
        '/bin/sh kubeadm init'
      ].join(';')
    end
  end
end
