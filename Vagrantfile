Vagrant.configure("2") do |config|
  # Use Ubuntu 22.04
  config.vm.box = "ubuntu/jammy64"

  # Resources: Give the VM 2GB of RAM
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  # Provisioning: Commands to run on the first 'vagrant up'
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    # Install Java 17 and Maven
    apt-get install -y openjdk-17-jdk maven
    
    # Install Docker (optional, since you mentioned Docker earlier)
    apt-get install -y docker.io
    usermod -aG docker vagrant
  SHELL
end
