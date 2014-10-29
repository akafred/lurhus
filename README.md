lurhus - a smarthouse setup
==============================

My personal smarthouse controller setup.

This setup uses [Vagrant](http://www.vagrantup.com/) to create the virtual machine I run the server in (so far I only run locally on my computer but in time I will change the setup to use a "server"). 

I use [Ansible](http://docs.ansible.com/) to automate provisioning of my virtual machine.


## My HW & SW

### Hardware:
  * Some machine to run Vagrant & virtualbox on - with two usb-slots available
  * AeoTec Z-Stick Series 2 - with Silicon Labs CP2102 USB to UART Bridge VCP (Virtual Com Port - USB Stick)
  * RFXCom Tranciever USB stick 
  * Netatmo
  * 4 Fibaro Wall plugs (Z-wave)
  * Aeon 4in1 sensor (Z-wave)
  * 3 Nexa wall plugs

### Software being setup by the stuff in this repo:
  * openHAB
  * HABmin

## Bootstrap and prereqs

1. Install virtualbox and vagrant:
    - Ubuntu:
        * `sudo apt-get install virtualbox`
        * vagrant > 1.5 - install deb manually: https://www.vagrantup.com/downloads.html
    - OSX: We recommend using [homebrew](http://brew.sh/) and [homebrew cask](http://caskroom.io/), but you can install these manually if you prefer (see download links).
        * `brew cask install virtualbox` -- or [Virtualbox Downloads](https://www.virtualbox.org/wiki/Downloads)
        * `brew cask install vagrant` -- or [Vagrant Downloads](https://www.vagrantup.com/downloads)
    - Windows:
        * Download and install "VirtualBox platform package" for Window hosts: [Virtualbox Downloads](https://www.virtualbox.org/wiki/Downloads)
        * Download and install Vagrant for Windows: [Vagrant Downloads](https://www.vagrantup.com/downloads)
        * Reboot your machine.
        * Install Cygwin by following this procedure: [Setting Up Cygwin](https://cygwin.com/install.html)
          - Choose the following packages:
            * git
            * openssh
          - We also recommend these:
            * curl
            * git-completion
            * tig
            * vim
            * wget
        * After installing Cygwin WIndows users should use a Cygwin Prompt for commands like git etc.
2. Clone this repo from the command line (in a directory of your choice):
   ```git clone https://github.com/akafred/lurhus.git```
3. `cd lurhus` into your cloned repo.
4. From the command line run: `vagrant up` to bootstrap the environment. Note! The repository contains file(s) encrypted using `ansible-vault` - in such files there are secrets - like netatmo binding keys etc. Without the passphrase to the encrypted files you cannot start the system - in other words you need to replace the files with your own encrypted files with your secrets - or remove the functionality.

After you are up and running, open a browser and point it to [openHAB http://localhost:8080/openhab.app](http://localhost:8080/openhab.app) or [HABmin http://localhost:8080/HABmin.app](http://localhost:8080/HABmin.app).


## Operations

### Deploying changes

In theory you should only ever need to use vagrant commands to update the virtual machine:

```
  vagrant up # to bootstrap the box initially
  vagrant provision # when you have changed something and want the virtual server updated
```

As long as you never tamper with the virtual machine manually you should be able to do `vagrant destroy && vagrant up` if anything misbehaves or you want to do a bigger upgrade. Of course this will loose any log persistent data you have collected (to be solved later).

### Log access

You can use the command `./show_logs.sh` to tail the openHAB logs.
