required_plugins = %w( vagrant-hostsupdater )
required_plugins.each do |plugin|
  exec "vagrant plugin install #{plugin};vagrant #{ARGV.join(" ")}" unless Vagrant.has_plugin? plugin || ARGV[0] == 'plugin'
end

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network :private_network, ip: '192.168.10.90'

  config.vm.hostname = "mail.local.example.io"
  config.hostsupdater.aliases = [ "autoconfig.mail.local.example.io" ]

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
