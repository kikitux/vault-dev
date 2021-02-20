# vault-dev

## description

This repo is my take on having a `vagrant` setup that I can use to create a `vault` in `dev` mode

## how to use this repo

In order to use this repo, the commands you need to run are

## INSTRUCTIONS

### Prerequisites

1. Install the latest version of [Vagrant](https://www.vagrantup.com/docs/installation)

2. Install [VirtualBox](https://www.virtualbox.org/)

### Clone the Repository

```shell
git clone https://github.com/kikitux/vault-dev.git
cd vault-dev
```

### What is included?

- A `Vagrantfile` that includes an Ubuntu VM
- A `download-vault.sh` script that will download Vault and Consul

[`Vagrantfile`](Vagrantfile) from this repository:
```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  config.vm.provision "shell", path: "scripts/download-vault.sh"
end
```

[`download-vault.sh`](scripts/download-vault.sh) from this repository:
```shell
#!/usr/bin/env bash

# download vault if not installed
# put it on /usr/local/bin


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
    echo vault_*.zip
    if [$? -ne 0 ]
    then
    wget https://releases.hashicorp.com/vault/1.6.1/vault_1.6.1_linux_amd64.zip
    fi

    # unzip vault into /usr/local/bin
    # add permissions to be executable
    unzip vault_1.6.1_linux_amd64.zip
    mv vault /usr/local/bin
    chmod +x /usr/local/bin/vault

    # add the HashiCorn GPG key
    curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -

    # add the oficial HashiCorp Linux repository
    sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"

    # install jq for json parsing
    sudo apt-get install jq

    # udpate and install Consul
    sudo apt-get update && sudo apt-get install consul

fi
```

### Start vagrant
```shell
vagrant up
```

### Check vault has been installed
```shell
which vault
```

### Connect to the VM
```shell
vagrant ssh
```

### Give yourself root permission
```shell
sudo su -
```

### Access the vagrant file created when the VM has started
```shell
cd /vagrant/
```

### Start the vault server in DEV mode
```shell
vault server -dev
```

TBC

## TODO
- [ ] have Alvaro review the README.md
 

## DONE
- [x] add `Vagrantfile`
- [x] write scripts that download `vault`
- [x] instruction how to use this repo
- [x] modify the script to install `consul`

