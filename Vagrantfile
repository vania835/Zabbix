# Vagrantfile
Vagrant.configure("2") do |config|
  
  # Машина 1 
  config.vm.define "controller" do |controller|
    controller.vm.box = "ubuntu/jammy64"
    controller.vm.network "private_network", ip: "192.168.56.10"

     # Настройка NAT для выхода в интернет
    controller.vm.network "public_network", type: "dhcp" # или используйте NAT по умолчанию VirtualBox, если это необходимо
    
    controller.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = "2"
      
    end
   
    
    controller.vm.provision "shell", inline: <<-SHELL
     
      sudo -i
      
      echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
      apt-get update
      sudo apt install docker-compose -y
      docker network create traefik-network
      docker network create zabbix-network
      docker-compose -f /vagrant/zabbix-traefik-letsencrypt-docker-compose/zabbix-traefik-letsencrypt-docker-compose.yml -p zabbix up -d

    SHELL

 
  end
  
 
end
