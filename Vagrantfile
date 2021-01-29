#!/usr/bin/env bash

# download vault if not installed
# put it on /usr/local/bin

Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  config.vm.provision "shell", path: "scripts/download-vault.sh"
end


which vault
if [ $? -ne 0 ]
then

    # check if unzip is installed
    # install unzip

    which unzip
    if [ $? -ne 0 ]
    then
        # unzip is not on path
        apt-get update
        apt-get install --yes unzip
    fi  

    # download vault.zip into /vagrant
    cd /vagrant
    wget https://releases.hashicorp.com/vault/1.6.1/vault_1.6.1_linux_amd64.zip

    # unzip vault into /usr/local/bin
    # add permissions to be executable
    unzip vault_1.6.1_linux_amd64.zip
    mv vault /usr/local/bin
    chmod +x /usr/local/bin/vault

fi
