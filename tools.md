#!/bin/bash

# Update package list
sudo apt-get update

# Install Microsoft Teams
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/ms-teams stable main"
sudo apt-get update
sudo apt-get install teams -y

# Install FortiClient VPN
wget https://filestore.fortinet.com/forticlient/downloads/FortiClientFullVPNInstaller_6.4.3.0851.deb
sudo dpkg -i FortiClientFullVPNInstaller_6.4.3.0851.deb
sudo apt-get install -f -y

# Install dependencies
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common -y

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Add Docker's stable repository
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Update package list (again)
sudo apt-get update

# Install Docker CE
sudo apt-get install docker-ce docker-ce-cli containerd.io -y

# Add current user to the docker group
sudo usermod -aG docker $USER
