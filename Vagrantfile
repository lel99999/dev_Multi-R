Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = "1024"
    v.cpus = 2
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "70"]
  end
# config.trigger.after :up do |trigger|
#   run "subscription-manager register --username <username> --password <password> --auto-attach
#   trigger.name = "After-Up Trigger ..."
#   trigger.info = "Trigger Execution ..."
#   trigger.run = { path:"subscription-manager register --username <username> --password <password> --auto-attach"}
# end

  config.vm.define :roletester do |roletester|
#   roletester.vm.box = "bento/centos-6.10"
#   roletester.vm.box = "clouddood/RH7.5_baserepo"
    roletester.vm.box = "clouddood/RH7.9_infra"
    roletester.vm.host_name = "roletester.test.dev"

    roletester.ssh.forward_agent = true

    roletester.vm.provision "ansible" do |ansible|
      ansible.playbook = "deploy_BaseSystem.yml"
      ansible.inventory_path = "vagrant_hosts"
#     ansible.tags = ansible_tags
#     ansible.verbose = ansible_verbosity
#     ansible.extra_vars = ansible_extra_vars
#     ansible.limit = ansible_limit
    end

#   roletester.vm.network :private_network, ip: "10.0.1.26"
    roletester.vm.network :private_network, ip: "192.168.60.25"
  end


#######################################################################################################################################

  ###########################
  ### R Server Component ###
  ###########################

  config.vm.define :r_server do |server|
#   server.vm.box = "bento/centos-6.10"
#   server.vm.box = "clouddood/RH7.5_baserepo"
    server.vm.box = "clouddood/RH7.9_infra"
    server.vm.host_name = "r-server.test.dev"

    server.ssh.forward_agent = true

    server.vm.provision "ansible" do |ansible|
#     ansible.playbook = "deploy_gocd.yml"
      ansible.playbook = "deploy_BaseSystem.yml"
      ansible.inventory_path = "vagrant_hosts"
#     ansible.tags = ansible_tags
#     ansible.verbose = ansible_verbosity
#     ansible.extra_vars = ansible_extra_vars
#     ansible.limit = ansible_limit
    end

#   server.vm.network :private_network, ip: "10.0.1.26"
    server.vm.network :private_network, ip: "192.168.60.26"
  end

end

