# -*- mode: ruby -*-
# vi: set ft=ruby :

WSVMBOX = 'ephillips/whonix-workstation'
GWVMBOX = 'ephillips/whonix-gateway'
HOST_IP = "10.152.152.10"
WSVBNME = "whonix-workstation"
GWVBNME = "whonix-gateway"
WSMEMOR = 4096
GWMEMOR = 512
WSCORES = 8
GWCORES = 2

Vagrant.configure(2) do |config|
    config.vm.define "gateway" do |gw|
      gw.vm.box = GWVMBOX
      gw.ssh.username = 'user'
      gw.vm.provider 'virtualbox' do |vb|
        vb.customize ['modifyvm', :id, '--memory', GWMEMOR]
        vb.customize ['modifyvm', :id, '--cpus', GWCORES]
        vb.gui = false
      end

      gw.vm.hostname = GWVBNME
      gw.vm.network "private_network", auto_config: false,
        virtualbox__intnet: "Whonix", adapter: 2
  
      gw.vm.network "forwarded_port", guest: 22, host: 2200, 
        id: "ssh", disabled: true
      gw.vm.network "forwarded_port", guest: 22, host: 2299
    end
  
    config.vm.define "workstation" do |ws|
      ws.vm.box = WSVMBOX
      ws.ssh.username = 'user'
      ws.ssh.host = HOST_IP
      ws.ssh.proxy_command = 'ssh user@127.0.0.1 -p 2299 -o '\
        'StrictHostKeyChecking=no -i ' + File.join(Dir.pwd(), 
          ".vagrant/machines/gateway/virtualbox/private_key") + 
         ' nc %h %p'
      ws.vm.provider 'virtualbox' do |vb|
        vb.customize ['modifyvm', :id, '--memory', WSMEMOR]
        vb.customize ['modifyvm', :id, '--cpus', WSCORES]
        vb.gui = false
      end
      ws.vm.boot_timeout = 160

      ws.vm.hostname = WSVBNME
      ws.vm.network "private_network", ip: HOST_IP, 
        virtualbox__intnet: "Whonix", adapter: 1
      ws.vm.network "forwarded_port", guest: 22, host: 2200,
        id: "ssh", disabled: true
  
      ws.ssh.forward_x11 = true
      ws.ssh.forward_env = ["DISPLAY"]
    end
  
    config.vm.synced_folder ".", "/vagrant", disabled: true
  end
