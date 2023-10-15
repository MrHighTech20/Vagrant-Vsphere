# Vagrant-Vsphere
Using vagrant to create VMs on Vsphere server 

Hey everone. I created a Vagrantfile to use with a vSphere (vCenter server). I had some problems to solve and I need to improve the code. First let's understand what we are doing in this case

# Vagrant
This guide explains how to set up a virtual machine (VM) using Vagrant with the VMware vSphere provider. Before I had to create the VM manually and saved it as a template in vCenter and the code creates a VM, based on that template and we will assign a fixed IP address and customize the SSH key for authentication.

## Prerequisites

Before you begin, ensure you have the following:

- [Vagrant](https://www.vagrantup.com/) installed
- Access to a VMware vCenter Server
- A Vagrant box for your desired OS
- Install vSphere plugin
```bash
  vagrant plugin install vagrant-vsphere
```
Access to a VMware vCenter Server
A Vagrant box for your desired OS

## Steps

1. **Create a Vagrant Project Directory**

   Create a new directory for your Vagrant project. Open your terminal and initialize the repository with the command:

```bash
  vagrant init
```

2. **Edit Vagrantfile**

```bash
  Vagrant.configure('2') do |config|
  config.vm.box = 'dummpy' # Use the appropriate Vagrant box name

# Configure network settings for a static IP in bridge mode
  config.vm.network 'public_network', bridge: 'VM Network'
  config.vm.network 'private_network', ip: '192.168.**.**' # Replace with your desired fixed IP

# Configure the vSphere provider settings
  config.vm.provider :vsphere do |vsphere|
    
# vSphere server settings
    vsphere.host = '192.168.**.**' # IP or hostname of the vSphere server
    vsphere.user = '@vsphere.local' # Username
    vsphere.password = 'YOUR PASSWORD' # Password
    vsphere.name = 'VM NAME' # Name of the virtual machine
    vsphere.compute_resource_name = 'Set your cluster or host' # Name of the vSphere cluster
    vsphere.template_name = 'Set you template' # Name of the template
    vsphere.insecure = true # Insecure mode (for self-signed certificates)

# SSH key and username settings
    config.ssh.private_key_path = 'Your user Path' # Path to the private key 
    config.ssh.insert_key = true
    config.ssh.username = 'ssh user' # SSH username

# Install VMTools
    config.vm.provision 'shell', inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y open-vm-tools
    SHELL
  end
end
```
Replace all placeholders with your actual values.

2. **Troubleshooting**

If you encounter issues with the vSphere provider settings, double-check your vSphere server credentials, permissions, and network configurations.

For more details on Vagrant and the vSphere provider, refer to the official documentation.
At the moment the VM is created using a template the would created before, after creating the virtual machine, Vagrant tried to create a connection using SSH but return one mensage saying:

```bash
default: SSH auth method: private key 
default: Warning: Authentication failure. Retrying...
```
The virtual machine is running but the not finished to config because the SSH not working.