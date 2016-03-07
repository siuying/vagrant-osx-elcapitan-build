Vagrant.configure(2) do |config|
  config.vm.box = 'carbon/osx-elcapitan-10.11'
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = "8096"
    vb.customize ["modifyvm", :id, "--usbehci", "off"]
  end

  config.push.define "atlas" do |push|
    push.app = "siuying/osx-build"
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo -u vagrant /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    sudo -u vagrant brew install ruby
    sudo -u vagrant brew install gitlab-ci-multi-runner
  SHELL
end
