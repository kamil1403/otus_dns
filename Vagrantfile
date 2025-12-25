Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |v|
    v.memory = 256
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  # Мастер-сервер ns01
  config.vm.define "ns01" do |ns01|
    ns01.vm.network "private_network", ip: "192.168.50.10", virtualbox__intnet: "dns"
    ns01.vm.hostname = "ns01"
  end

  # Клиент 1
  config.vm.define "client" do |client|
    client.vm.network "private_network", ip: "192.168.50.15", virtualbox__intnet: "dns"
    client.vm.hostname = "client"
  end

  # Клиент 2
  config.vm.define "client2" do |client2|
    client2.vm.network "private_network", ip: "192.168.50.16", virtualbox__intnet: "dns"
    client2.vm.hostname = "client2"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.become = "true"
  end
end
