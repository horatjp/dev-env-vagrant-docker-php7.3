Vagrant.configure(2) do |config|

  config.vm.box = "ailispaw/barge"

  config.disksize.size = '30GB'

  config.vm.provider :virtualbox do |v|
    v.memory = 2048
    v.cpus = 2


    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root","1"]
  end

  config.vm.network "private_network", type: "dhcp", ip: "192.168.33.0"

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ip_resolver = proc do |vm, resolving_vm|
    ip_address = ''
    if hostname = (vm.ssh_info && vm.ssh_info[:host])
      vm.communicate.execute("/sbin/ifconfig eth1 | grep 'inet addr' | tail -n 1 | egrep -o '[0-9\.]+' | head -n 1 2>&1") do |type, contents|
        ip_address = contents.split("\n").first
      end
    end
    ip_address
  end

  config.hostmanager.aliases = ["phpdev.test"]

  config.vm.synced_folder ".", "/vagrant", type:"virtualbox", create: true

  config.vm.provision "shell", inline: "/etc/init.d/docker restart 19.03.5", privileged: true

  # docker-compose
  config.vm.provision :shell, inline: <<-SHELL
    wget -L https://github.com/docker/compose/releases/download/1.25.3/docker-compose-`uname -s`-`uname -m` -O ~/docker-compose
    sudo mv ~/docker-compose /opt/bin/docker-compose
    sudo chown root:root /opt/bin/docker-compose
    sudo chmod +x /opt/bin/docker-compose
  SHELL


  config.vm.provision "shell", privileged: false, inline: <<-SHELL

    if ! grep 'cd /vagrant' ~/.bashrc;
    then
        echo 'cd /vagrant' >> ~/.bashrc
        source ~/.bashrc
    fi
  SHELL

  config.vm.provision "shell", run: 'always', privileged: false, inline: <<-SHELL
    cd /vagrant && docker-compose up -d 1>&2
  SHELL
end
