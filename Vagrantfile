Vagrant.configure(2) do |config|

    config.vm.box = "ubuntu/bionic64"

    config.vm.define "load-balancer" do |loadbalancer|
      loadbalancer.vm.network "private_network", ip: "192.168.33.11"
      loadbalancer.vm.hostname = "load-balancer"
      loadbalancer.vm.network "forwarded_port", guest: 80, host: 8080
      loadbalancer.vm.provider "virtualbox" do |vb| 
        vb.memory = 512
        vb.customize ["modifyvm", :id, "--audio", "none"]
      end


      loadbalancer.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "ansible/site.yml"
        ansible.become = true
        ansible.inventory_path = "ansible/hosts"
      end 

    end

    config.vm.define "server-1" do |server_1|
      server_1.vm.network "private_network", ip: "192.168.33.12"
      server_1.vm.hostname = "server-1"
      server_1.vm.provider "virtualbox" do |vb| 
        vb.memory = 512
        vb.customize ["modifyvm", :id, "--audio", "none"]
      end


      server_1.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "ansible/site.yml"
        ansible.become = true
        ansible.inventory_path = "ansible/hosts"
      end

    end   


    config.vm.define "server-2" do |server_2|
      server_2.vm.network "private_network", ip: "192.168.33.13"
      server_2.vm.hostname = "server-2"
      server_2.vm.provider "virtualbox" do |vb| 
        vb.memory = 512
        vb.customize ["modifyvm", :id, "--audio", "none"]
      end


      server_2.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "ansible/site.yml"
        ansible.become = true
        ansible.inventory_path = "ansible/hosts"
      end
    end 

    config.vm.define "db" do |db|
      db.vm.box = "ubuntu/bionic64"
      db.vm.hostname = "db"
      db.vm.network "private_network", ip: "192.168.33.30"
      db.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.cpus = "1"
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      end
      db.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbooks/db.yml"
      end
    end

    config.vm.provision "shell", inline: <<-SHELL   
      apt-get update
    SHELL

end