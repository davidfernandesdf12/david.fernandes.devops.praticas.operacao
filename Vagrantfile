Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "servidor-web"


  # Interface de rede privada com IP estático
  config.vm.network "private_network", type: "static", ip: "192.168.10.10"
  config.vm.network "public_network", type: "dhcp"


  # Porta 80 da máquina virtual para a porta 8080 da máquina local
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # Configurações do Provedor
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 1

  end

  # Configurações do Diretorio Compartilhado

  config.vm.synced_folder "./shared_windows", "/shared_linux"


  # Configurações de Shell

  config.vm.provision "shell", inline: <<-SHELL

    apt-get update

    apt-get install -y apache2 htop nano python3

    echo "ServerName servidor-web" >> /etc/apache2/apache2.conf

    systemctl start apache2

    ufw allow 8080/tcp

    systemctl start apache2

    systemctl enable apache2

  SHELL

end