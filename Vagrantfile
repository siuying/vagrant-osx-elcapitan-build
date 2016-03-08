Vagrant.configure(2) do |config|
  config.vm.box = 'carbon/osx-elcapitan-10.11'
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = "8096"
    vb.customize ["modifyvm", :id, "--usbehci", "off"]
    vb.cpus = `sysctl -n hw.physicalcpu`.strip.to_i

    # setup serial so that we can install apps needed
    # http://zhiwei.li/text/2015/10/08/virtualbox%E5%AE%89%E8%A3%85el-capitan/
    vb.customize ["setextradata", :id, "VBoxInternal/Devices/efi/0/Config/DmiSystemUuid", "C0EC81E9-6729-11E1-8B14-502690982710"]
    vb.customize ["setextradata", :id, "VBoxInternal/Devices/efi/0/Config/DmiSystemSerial", "C02MM34SG3QT"]
    vb.customize ["setextradata", :id, "VBoxInternal/Devices/efi/0/Config/DmiBoardSerial", "CK148614DB6F940D2"]
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo -u vagrant /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    sudo -u vagrant brew install ruby
    sudo -u vagrant brew install carthage
    sudo -u vagrant brew install gitlab-ci-multi-runner
    sudo -u vagrant gem install bundler
  SHELL
end
