Vagrant.require_version ">= 1.5"
Vagrant.configure("2") do |config|

    config.vm.box = "centos64-x86_64-20131030"
    config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v0.1.0/centos64-x86_64-20131030.box"
    config.vm.synced_folder "./", "/vagrant", type: "nfs"

    config.vm.provider :virtualbox do |v|
        v.name = "default"
        v.customize [
            "modifyvm", :id,
            "--name", "default",
            "--memory", 512,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end


    config.vm.network "private_network", type: "dhcp"
    config.ssh.forward_agent = true
    config.vm.network :forwarded_port, guest: 4200, host: 4200
    config.vm.network :forwarded_port, guest: 49152, host: 49152
    # If ansible is in your path it will provision from your HOST machine
    # If ansible is not found in the path it will be instaled in the VM and provisioned from there
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.limit = 'all'
    end
end
