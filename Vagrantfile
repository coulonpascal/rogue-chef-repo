# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
BERKSHELF = false

# We'll mount the Chef::Config[:file_cache_path] so it persists between
# Vagrant VMs
host_cache_path = File.expand_path("../.cache", __FILE__)
guest_cache_path = "/tmp/vagrant-cache"

# ensure the cache path exists
FileUtils.mkdir(host_cache_path) unless File.exist?(host_cache_path)

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "trusty64"

  # Install RVM, Ruby and Chef on the Virtual Machine.
  unless BERKSHELF

    ######################## NOTE ############################
    # the parameter passed to geoshape-install.sh will indicate which version of geoshape will be installed. 
    # for example "release-1.5" will get the tag release-1.5 on the rogue-chef-repo and install everything
    # according to that releases' corresponding component versions. if a tag, commit id, or branch is not 
    # specified to indicate which version to install, the newest 'release-xxxx' will be installed. if you want
    # the latest development version you need to pass in 'master' otherwise not passing a version will get
    # the latest release
    config.vm.provision :shell, :path => "scripts/geoshape-install.sh", :args => "vagrant release-1.8"
  end

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  # trusty64

  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network :forwarded_port, guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP. If you want to run multiple vms at once, you can change the .100 
  # running a private network eliminates the chances of conflicting with the network you are connected to. 
  # this is particularly useful when you want to run the vm on your laptop and endup being on various networks
  # or even no network connectivity 
  config.vm.network :private_network, ip: "192.168.99.100"

  # Create a public network, obtain it's ip through dhcp and bridge it through host's en0
  # config.vm.network :public_network, :bridge => 'en0: Ethernet'

  # The following can be used to specify a static ip through the host's  en0. You can use other nework adaptors such as 'en1: Wi-Fi (AirPort)'  
  # config.vm.network :public_network, :bridge => 'en0: Ethernet', ip: "192.168.10.222", netmask: "255.255.255.0"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider :virtualbox do |vb|
    # Don't boot with headless mode
    vb.gui = true
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "8096"]
    vb.customize ["modifyvm", :id, "--cpus", "2"]
  end
  #
  # View the documentation for the provider you're using for more
  # information on available options.

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #

end
