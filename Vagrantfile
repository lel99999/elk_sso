Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = "1024"
    v.cpus = 2
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "70"]
  end
  config.vm.define "winELKAD01" do |winELKAD01|
    winELKAD01.vm.box = "https://app.vagrantup.com/mwrock/boxes/Windows2012R2"
#   winELKAD01.vm.box = "mwrock/Windows2012R2"
    winELKAD01.vm.hostname = "winEOD01"
    winELKAD01.vm.network "private_network", ip: "192.168.60.170"
  end

  config.vm.define "elkrh7" do |elkrh7|
    #elkrh7.vm.box = "generic/rhel7"
    elkrh7.vm.box = "iamseth/rhel-7.3"
    #elkrh7.vm.box = "javier-lopez/rhel-7.4"
    #elkrh7.vm.box = "xianlin/rhel-7.4"
    elkrh7.vm.hostname = "elkrh7"
    elkrh7.vm.network "private_network", ip: "192.168.60.172"
    elkrh7.vm.provision "shell", :inline => "sudo echo '192.168.60.172 elkrh7.local elkrh7' >> /etc/hosts"
    elkrh7.vm.provision "shell", :inline => "sudo echo '192.168.60.173 elkapp7.local elkapp7' >> /etc/hosts"
         
    elkrh7.vm.provision "ansible" do |ansible|
      ansible.playbook = "deploy_elkrh7.yml"
      ansible.inventory_path = "vagrant_hosts"
      #ansible.tags = ansible_tags
      #ansible.verbose = ansible_verbosity
      #ansible.extra_vars = ansible_extra_vars
      #ansible.limit = ansible_limit
    end
  end
end
