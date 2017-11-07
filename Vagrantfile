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

      srv.vm.provider "vmware_fusion" do |v|
        v.gui = false
        v.linked_clone = false
        v.name = servers["name"]
        v.vmx["memsize"] = servers["ram"]
        v.vmx["numvcpus"] = "2"
      end
    end
  end
end
