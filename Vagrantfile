
Vagrant.configure("2") do |config|

  config.vm.box_download_insecure=true
  config.vm.box = "ubuntu/bionic64"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end
  config.vm.define "ci-server" do |ciServer|
    ciServer.vm.network "private_network", ip:'192.168.56.60'
    ciServer.vm.hostname = "ci-server"
  end

  config.vm.define "server-2" do |server2|
    server2.vm.network "private_network", ip:'192.168.56.70'
    server2.vm.hostname = "server-2"
    server2.vm.provision :docker
    server2.vm.provision :docker_compose
    server2.vm.provision :file, source: "AT20_CONVERT_SERVICE_TS", destination: "AT20_CONVERT_SERVICE_TS"
    server2.vm.provision "shell", inline: "docker compose -f /home/vagrant/AT20_CONVERT_SERVICE_TS/docker-compose.yaml up -d"
  end
end
