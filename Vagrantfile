# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  if Vagrant.has_plugin?("vagrant-proxyconf")
		if ENV["http_proxy"]
		  	puts "http_proxy: " + ENV["http_proxy"]
		  	config.proxy.http     = ENV["http_proxy"]
		end
		if ENV["https_proxy"]
		    puts "https_proxy: " + ENV["https_proxy"]
		    config.proxy.https    = ENV["https_proxy"]
		end
		if ENV["no_proxy"]
		    config.proxy.no_proxy = ENV["no_proxy"]
		end
  end
  
  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "33.33.33.10"
  config.vm.host_name = "oraxe"
  config.vm.provision :puppet, :module_path => "modules", :options => "--verbose --trace" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file  = "site.pp"
  end
  config.vm.provider "virtualbox" do |vb|
     vb.gui = false
     vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
     vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
     vb.customize ["modifyvm", :id, "--name", "dev_env_oraxe"]
     vb.customize ["modifyvm", :id, "--memory", "2048"]
  end
end
