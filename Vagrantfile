Vagrant.configure("2") do |config|

    #############################################################
    # Local Virtual box Provider
    #############################################################
    config.vm.provider :virtualbox do |v|
        v.name = "odoo.app"
        v.customize ["modifyvm", :id, "--memory", 1024]
        config.vm.box = "ubuntu/trusty64"
        config.vm.network :private_network, ip: "192.168.13.37"
        config.ssh.forward_agent = true

        config.vm.network :forwarded_port, host: 33060, guest: 3306
    end

    #############################################################
    # Ansible provisioning (you need to have ansible installed)
    #############################################################
    
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.inventory_path = "ansible/inventories/dev"
        ansible.limit = 'all'
    end
    
    config.vm.synced_folder "./", "/vagrant", type: "nfs"
end
