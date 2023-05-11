
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
    server2.vm.provision :file, source: "docker-compose.yaml", destination: "docker-compose.yaml"
    server2.vm.provision :file, source: ".env", destination: ".env"
    server2.vm.provision :file, source: "Dockerfile", destination: "Dockerfile"
    server2.vm.provision :file, source: ".dockerignore", destination: ".dockerignore"
    server2.vm.provision :file, source: "index.ts", destination: "index.ts"
    server2.vm.provision :file, source: "src", destination: "src"
    server2.vm.provision :file, source: "package.json", destination: "package.json"
    server2.vm.provision :file, source: "package-lock.json", destination: "package-lock.json"
    server2.vm.provision :file, source: "tsconfig.json", destination: "tsconfig.json"
    server2.vm.provision "shell", inline: "docker compose up -d"
  end
end
