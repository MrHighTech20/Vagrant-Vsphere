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

    config.vm.provision 'shell', inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y open-vm-tools
    SHELL
  end
end