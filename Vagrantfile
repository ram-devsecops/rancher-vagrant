# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

require 'yaml'
@servers = YAML.load_file('.servers.yml')
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false
  @servers.each do |servers|
    config.vm.define servers["name"] do |srv|
      srv.vm.box          = servers["box"]
      srv.vm.communicator = servers["communicator"]
      srv.vm.boot_timeout = 1600
      srv.vm.hostname     = servers["hostname"]

      srv.vm.provider :virtualbox do |v|
        if servers["communicator"] != "winrm"
        v.gui    = false
        else
        v.gui = true
        end
        v.name   = servers["name"]
        v.memory = servers["ram"]
        v.cpus   = 2
      end
    end
  end
end
