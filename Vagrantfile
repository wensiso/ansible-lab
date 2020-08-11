#!/usr/bin/ruby

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  #config.vm.box = "hashicorp/precise64"
  vmbox_ubuntu = "generic/ubuntu2004" 
  vmbox_debian = "debian/buster64"
  vmbox_centos = "centos/8"
  vmbox_version_centos = "1905.1"
 
  config.vm.boot_timeout = 120
  config.vm.define "ansible" do |ansible|
    ansible.vm.box = vmbox_ubuntu
    ansible.vm.hostname = 'ansible'
    ansible.vm.network :private_network, :ip => '192.168.15.100'
  end

  config.vm.define "centos" do |centos|
    centos.vm.box = vmbox_centos
    centos.vm.box_version = vmbox_version_centos
    centos.vm.hostname = 'centos'
    centos.vm.network :private_network, :ip => '192.168.15.101'
  end

  config.vm.define "debian" do |debian|
    debian.vm.box = vmbox_debian
    debian.vm.hostname = 'debian'
    debian.vm.network :private_network, :ip => '192.168.15.102'
  end

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "/home/wendell", "/home/vagrant/home-host", type: 'nfs', nfs_udp: false, nfs_version: 4
  
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  config.vm.provider :libvirt do |libvirt|

    # A hypervisor name to access. Different drivers can be specified, but
    # this version of provider creates KVM machines only. Some examples of
    # drivers are KVM (QEMU hardware accelerated), QEMU (QEMU emulated),
    # Xen (Xen hypervisor), lxc (Linux Containers),
    # esx (VMware ESX), vmwarews (VMware Workstation) and more. Refer to
    # documentation for available drivers (http://libvirt.org/drivers.html).
    libvirt.driver = "kvm"
    libvirt.cpus = 2
    libvirt.memory = 512
  end

  
  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  
  config.vm.define "ansible" do |ansible|
     ansible.vm.provision "shell", inline: <<-SHELL
        echo "Updating /etc/apt/sources.list"
        sudo cat /dev/null > /etc/apt/sources.list
        echo "deb http://repositorio.nti.ufal.br/ubuntu/ focal main restricted" >> /etc/apt/sources.list
        echo "deb http://repositorio.nti.ufal.br/ubuntu/ focal-updates main restricted" >> /etc/apt/sources.list
        echo "#########" >> /etc/apt/sources.list
        echo "deb http://repositorio.nti.ufal.br/ubuntu/ focal universe" >> /etc/apt/sources.list
        echo "deb http://repositorio.nti.ufal.br/ubuntu/ focal-updates universe" >> /etc/apt/sources.list
        echo "#########" >> /etc/apt/sources.list
        echo "deb http://repositorio.nti.ufal.br/ubuntu/ focal multiverse" >> /etc/apt/sources.list
        echo "deb http://repositorio.nti.ufal.br/ubuntu/ focal-updates multiverse" >> /etc/apt/sources.list
        echo "#########" >> /etc/apt/sources.list
        echo "deb http://repositorio.nti.ufal.br/ubuntu/ focal-backports main universe multiverse restricted" >> /etc/apt/sources.list
        echo "#########" >> /etc/apt/sources.list
        echo "deb http://repositorio.nti.ufal.br/ubuntu/ focal-security main restricted" >> /etc/apt/sources.list
        echo "deb http://repositorio.nti.ufal.br/ubuntu/ focal-security universe" >> /etc/apt/sources.list
        echo "deb http://repositorio.nti.ufal.br/ubuntu/ focal-security multiverse" >> /etc/apt/sources.list
        echo "#########" >> /etc/apt/sources.list
        echo "Running apt-get update"
        sudo apt-get update
        sudo apt-get update
        echo "Installing utils"
        sudo apt-get install -y vim htop net-tools tree python3-pip
        echo "Finished!"
     SHELL
  end
end
