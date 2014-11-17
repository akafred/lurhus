# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "puphpet/debian75-x64"

  config.ssh.forward_x11 = true
  config.ssh.forward_agent = true

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize ["modifyvm", :id, "--usbehci", "off"]
    vb.customize ['usbfilter', 'add', '0', '--target', :id, '--name', 'Z-Stick S2', '--vendorid', '0x10c4', '--productid', '0xea60']
    vb.customize ['usbfilter', 'add', '0', '--target', :id, '--name', 'RFXCOM', '--vendorid', '0x0403', '--productid', '0x6001']
  end
  
  config.vm.network "forwarded_port", guest: 8080, host: 8080, auto_correct: true

  # http://fgrehm.viewdocs.io/vagrant-cachier
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.ask_vault_pass = true
    ansible.verbose = "vv"
  end

end
