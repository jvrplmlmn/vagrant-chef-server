Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/trusty"

  config.vm.provider "virtualbox" do |vbox, override|
    vbox.customize ["modifyvm", :id, "--memory", "4096"]
    vbox.customize ["modifyvm", :id, "--cpus", "4"]

    override.vm.network :private_network, ip: "192.168.33.10"

    override.vm.network :forwarded_port, guest: 80, host: 80
    override.vm.network :forwarded_port, guest: 443, host: 443
  end

  config.vm.provision :shell, :privileged => true, :inline => <<-SCRIPT
    VERSION=12.4.1-1
    PACKAGE="chef-server-core_${VERSION}_amd64.deb"
    wget --no-check-certificate https://packages.chef.io/stable/ubuntu/14.04/${PACKAGE} -O /vagrant/${PACKAGE}
    dpkg -i /vagrant/${PACKAGE}
    chef-server-ctl reconfigure
  SCRIPT

end
