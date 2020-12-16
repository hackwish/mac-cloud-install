
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'virtualbox'

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vagrant.plugins = [
      "sahara",
      "vagrant-cachier",
      "vagrant-exec",
      "vagrant-hostmanager",
      "vagrant-hosts",
      "vagrant-list",
      "vagrant-mutate",
      "vagrant-scp",
      "vagrant-vbguest",
      "vocker",
    ]
    config.vm.define "macosx-test"
    config.vm.box = "ramsey/macos-catalina" # "yzgyyang/macOS-10.14"

    # Use NFS for the shared folder
    #   config.vm.synced_folder ".", "/vagrant",
    #     id: "core",
    #     :nfs => true,
    #     :mount_options => ['nolock,vers=3,udp,noatime,actimeo=1,resvport'],
    # :export_options => ['async,insecure,no_subtree_check,no_acl,no_root_squash']

     # NFS needs host-only network
    config.vm.network :private_network, ip: "172.16.200.100"

    config.vm.provider :virtualbox do |virtualbox|
        virtualbox.name = "macosx-test"
        virtualbox.memory = 4096
        virtualbox.cpus = 2
        # Show gui, incl. some power
        virtualbox.gui = true

        # Some needed OSX configs
        virtualbox.customize ["modifyvm", :id, "--cpuid-set", "00000001", "000106e5", "00100800", "0098e3fd", "bfebfbff"]
        virtualbox.customize ["setextradata", :id, "VBoxInternal/Devices/efi/0/Config/DmiSystemProduct", "MacBookPro11,3"]
        virtualbox.customize ["setextradata", :id, "VBoxInternal/Devices/efi/0/Config/DmiSystemVersion", "1.0"]
        virtualbox.customize ["setextradata", :id, "VBoxInternal/Devices/efi/0/Config/DmiBoardProduct", "Iloveapple"]
        virtualbox.customize ["setextradata", :id, "VBoxInternal/Devices/smc/0/Config/DeviceKey", "ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc"]
        virtualbox.customize ["setextradata", :id, "VBoxInternal/Devices/smc/0/Config/GetKeyFromRealSMC", "1"]

        # set resolution on OSX:
        # 0,1,2,3,4,5 :: 640x480, 800x600, 1024x768, 1280x1024, 1440x900, 1920x1200
        virtualbox.customize ["setextradata", :id, "VBoxInternal2/EfiGopMode", "4"]
    end
    
    #ANSIBLE
    # config.vm.provision :shell, :inline => "cd /vagrant/"
    # config.vm.provision :shell, :inline => "/vagrant/install.sh"
end