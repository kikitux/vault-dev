
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  config.vm.provision "shell", path: "https://raw.githubusercontent.com/kikitux/curl-bash/master/vault-dev-inmem/vault.sh"
  config.vm.provision "shell", path: "https://raw.githubusercontent.com/kikitux/curl-bash/master/provision/terraform.sh"
  config.vm.network "forwarded_port", guest: 8200, host: 8200
end
