Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network :private_network, ip: '192.168.10.90'

  config.vm.hostname = "local.dave.io"
  config.hostsupdater.aliases = [ "autoconfig.local.dave.io", "local.dave.io", "mail.local.dave.io" ]

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "tests/test.yml"
  end

  config.vm.provider "virtualbox" do |v|
    v.memory = 512
    v.cpus = 1
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    # change the network card hardware for better performance
    v.customize ["modifyvm", :id, "--nictype1", "virtio" ]
    v.customize ["modifyvm", :id, "--nictype2", "virtio" ]
  end

end
