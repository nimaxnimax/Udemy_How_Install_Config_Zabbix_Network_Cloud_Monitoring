![Alt text](image.png)

Udemy Course >> How Install Config Zabbix 6 Network Cloud Monitoring Part 1

**********

Complete Crash Course >> Server Network Administration Cloud Monitoring for Free Zabbix 6 for Monitoring Cloud Router Switch Windows Linux VPS P1 (Azure Cloud Test Lab and Local VMware & Virtual-Box Test Lab)

**********

Tips/Tricks/Notes/Commands URL Link:



Instructor & Courses:

https://www.udemy.com/user/adrian-fischer-infotech/

**********

Lab Requirements:

Option 1 - Cloud
- Azure >> https://azure.microsoft.com/en-us/get-started/azure-portal
- AWS >> https://aws.amazon.com/
- GCP >> https://cloud.google.com/free
- Digitalocean >> https://www.digitalocean.com/

Option 2 - PC Virtualization Options - Installation/Download URL Links (Windows/Linux/Mac):
- VMware Player >> https://www.vmware.com/uk/products/workstation-player/workstation-player-evaluation.html
- Virtual-Box >> https://www.virtualbox.org/wiki/Downloads
- Vagrant >> https://developer.hashicorp.com/vagrant/install
- Ubuntu Download Link >> https://releases.ubuntu.com/jammy/

**********


**********


**********

Swap Configuration on Ubuntu 20 or 22 - Linux Command >>
```bash
sudo apt update -y && sudo apt upgrade -y
sudo lsb_release -a
sudo apt install screen -y
sudo fallocate -l 4G /swapfile
ls -anp /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

**********

VB and Vagrant Installation on Ubuntu 22 - Linux Command >>
```bash
sudo apt update -y && sudo apt upgrade -y
wget https://www.virtualbox.org/download/oracle_vbox_2016.asc
cat oracle_vbox_2016.asc | gpg --dearmor | sudo tee /usr/share/keyrings/virtualbox.gpg > /dev/null 2>&1
echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/virtualbox.gpg] https://download.virtualbox.org/virtualbox/debian jammy contrib' | sudo tee -a /etc/apt/sources.list.d/virtualbox.list
sudo apt update && sudo apt install virtualbox-7.0 -y
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant -y
```

```bash
sudo vi Vagrantfile
```

```bash
Vagrant.configure("2") do |config|
    config.vm.define "ubuntu1" do |node|
        node.vm.box = "generic/ubuntu2204"
        node.vm.hostname = "ubuntu1"
        config.vm.network "public_network"
        config.vm.provider "virtualbox" do |vb|
            vb.gui = false
            vb.memory = "1024"
        end
    end
end
```

```bash
Vagrant.configure("2") do |config|
    config.vm.define "ubuntu1" do |node|
        node.vm.box = "generic/ubuntu2204"
        node.vm.hostname = "ubuntu1"
        config.vm.network "public_network"
        config.vm.provider "virtualbox" do |vb|
            vb.gui = false
            vb.memory = "1024"
        end
    end
    config.vm.define "ubuntu2" do |node|
        node.vm.box = "generic/ubuntu2204"
        node.vm.hostname = "ubuntu2"
        config.vm.network "public_network"
        config.vm.provider "virtualbox" do |vb|
            vb.gui = false
            vb.memory = "1024"
        end
    end
    config.vm.define "ubuntu3" do |node|
        node.vm.box = "generic/ubuntu2204"
        node.vm.hostname = "ubuntu3"
        config.vm.network "public_network"
        config.vm.provider "virtualbox" do |vb|
            vb.gui = false
            vb.memory = "1024"
        end
    end
end
```

```bash
cat Vagrantfile
```

```bash
vagrant help
vagrant global-status
vagrant up
vagrant ssh [ID]
vagrant destroy [ID]
```

