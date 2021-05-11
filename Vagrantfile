Vagrant.configure("2") do |config|
    ##### test empty linux box #####
    # empty linux 
    # 연습으로 깡통 리눅스만 올려 봅니다. 
    # vagrant up empty 명령이 실행 완료되면, 리눅스 가상머신이 생성됩니다.
    # vagrant ssh empty 로 리눅스 운영체제에 콘솔 연결할 수 있습니다. 
    config.vm.define "empty" do |vname|
        vname.vm.box = "ubuntu/trusty64"
        vname.vm.hostname = "empty"

        vname.trigger.before :halt do |trigger|
            trigger.warn = "resource clearing before halt."
            trigger.run_remote = {inline: "echo ..."}
        end

        vname.vm.provider "virtualbox" do |vb|
            vb.name = "empty"
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
