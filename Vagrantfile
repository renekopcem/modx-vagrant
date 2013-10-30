Vagrant.configure("2") do |config|
  config.vm.box = "default2"
  config.vm.box_url = "http://files.vagrantup.com/precise64_vmware.box"

  config.vm.network :private_network, ip: "172.10.0.200", :netmask => "255.255.0.0"
  config.vm.synced_folder "./", "/var/www", id: "vagrant-root", :nfs => true

  config.vm.provision :shell, :path => "shell/initial-setup.sh"
  config.vm.provision :shell, :path => "shell/update-puppet.sh"
  config.vm.provision :shell, :path => "shell/librarian-puppet-vagrant.sh"
  config.vm.provision :puppet do |puppet|
    puppet.facter = {
      "ssh_username" => "vagrant"
    }

    puppet.manifests_path = "puppet/manifests"
    puppet.options = ["--verbose", "--hiera_config /vagrant/hiera.yaml", "--parser future"]
  end

end

