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
