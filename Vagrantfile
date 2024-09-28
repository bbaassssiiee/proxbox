# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "clincha/proxmox-ve-8"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = true

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 8006, host: 8006, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  config.vm.network "public_network", type: "dhcp", bridge: "en0: Wi-Fi"
  config.vm.disk :disk, name: "proxmox", size: "100GB"
  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessible to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.hostname = "pve"
  config.vm.define "pve" do |pve|
    pve.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.default_nic_type = "82540em"
      vb.customize ["modifyvm", :id,
        "--audio-driver", "none",
        "--cpus", 8,
        "--firmware", "EFI",
        "--macaddress2", "00C0DEDEC0DE",
        "--memory", 16384,
        "--name", "pve",
        "--graphicscontroller", "VMSVGA",
        "--vram", "64",
        "--vrde", "on"
      ]
      vb.customize ["storageattach", :id,
        "--device", "0",
        "--medium", "emptydrive",
        "--port", "1",
        "--storagectl", "IDE Controller",
        "--type", "dvddrive"
      ]
    end
  end
  config.vm.provision :ansible do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "ansible/vagrant.yml"
    ansible.verbose = "v"
    end
  end
end
