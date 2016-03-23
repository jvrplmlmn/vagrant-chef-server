Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/trusty"

  config.vm.provider "virtualbox" do |vbox, override|
    vbox.customize ["modifyvm", :id, "--memory", "4096"]
    vbox.customize ["modifyvm", :id, "--cpus", "4"]

    override.vm.network :private_network, ip: "192.168.33.10"

    override.vm.network :forwarded_port, guest: 80, host: 80
    override.vm.network :forwarded_port, guest: 443, host: 443
  end

end
