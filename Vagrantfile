# -*- mode: ruby -*-
# vi: set ft=ruby :

# process arguments for glu
# getoptlong removes arguments from ARGV which is required by vagrant
require 'getoptlong'
opts = GetoptLong.new(
  [ '--glu-version', GetoptLong::OPTIONAL_ARGUMENT ]
)
gluVersion=''
opts.each do |opt, arg|
  case opt
    when '--glu-version'
      gluVersion=arg
  end
end

Vagrant.configure("2") do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu-12.04-chef-puppet"
 
  # veewee box url
  config.vm.box_url = "https://www.dropbox.com/s/9dp4is853nuix87/ubuntu-12.04-chef-puppet.box"
  # Set hostname
  config.vm.hostname = "glu-tutorial"
  
  # Forward ports

  # apache frontend to glu console webapp
  config.vm.network :forwarded_port, guest: 8000, host: 8000

  # glu console 
  config.vm.network :forwarded_port, guest: 8080, host: 8080

  # webapp1
  config.vm.network :forwarded_port, guest: 9000, host: 9000

  # webapp2
  config.vm.network :forwarded_port, guest: 9001, host: 9001

  # webapp3
  config.vm.network :forwarded_port, guest: 9002, host: 9002

  # Set system settings
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"]
    vb.customize ["modifyvm", :id, "--cpus", "1"]
  end

  config.vm.provision :shell do |s|
    s.path = "install-glu.sh"
    s.args = "#{gluVersion}"
  end
end
