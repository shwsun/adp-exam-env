Vagrant.configure("2") do |config|
    # installed in /opt/vagrant/embedded .... gemrc 
    # https://cloud.centos.org/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-2004_01.VirtualBox.box
    # vagrant box add centos/7 CentOS-7-x86_64-Vagrant-2004_01.VirtualBox.box
    # config.vbguest.auto_update = false
    # test linux 
    # 연습으로 깡통 리눅스만 올려 봅니다. 
    # vagrant up test 명령이 실행 완료되면, 리눅스 가상머신이 생성됩니다.
    # vagrant ssh test 로 리눅스 운영체제에 콘솔 연결할 수 있습니다. 
    config.vm.define "test" do |vname|
        vname.vm.box = "centos/7"
        vname.vm.hostname = "test"

        vname.trigger.before :halt do |trigger|
            trigger.warn = "Dumping database to /vagrant/outfile"
            trigger.run_remote = {inline: "echo AAAA"}
        end

        vname.vm.provider "virtualbox" do |vb|
            vb.name = "test"
            vb.customize ['modifyvm', :id, '--audio', 'none']
            vb.memory = 1000
            vb.cpus = 2
        end
        vname.vm.network "private_network", ip: "192.168.56.20"
    end

    # Jupyter Notebook
    # http://192.168.56.23:8888 
    config.vm.define "jup" do |vname|
        vname.vm.box = "centos/7"
        vname.vm.hostname = "jup"
        vname.vm.provider "virtualbox" do |vb|
            vb.name = "jup"
            vb.customize ['modifyvm', :id, '--audio', 'none']
            vb.memory = 1000
            vb.cpus = 2
        end
        vname.vm.network "private_network", ip: "192.168.56.23"
        vname.vm.network "forwarded_port", guest: 8888, host: 8888
        # provisioning

        vname.vm.provision "shell", path: "./shells/boot_jupyter.sh", run: "once"
        vname.vm.provision "shell", path: "./shells/start_jupyter.sh", run: "always"
    end


end
