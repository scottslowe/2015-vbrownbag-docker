# Building a CoreOS etcd Cluster with Vagrant

These files are intended to allow users to use Vagrant to quickly spin up a cluster of CoreOS virtual machines (VMs) running etcd. This configuration was tested using Vagrant 1.7.2, VMware Fusion 6.0.5, and the Vagrant VMware plugin.

## Contents

* **README.md**: This file that you're reading now.

* **Vagrantfile**: This file is used by Vagrant to spin up the virtual machines. This file is fairly extensively commented to help explain what's happening. You should be able to use this file unchanged; all the VM configuration options are stored outside this file.

* **servers.yml**: This YAML file contains a list of VM definitions. It is referenced by `Vagrantfile` when Vagrant instantiates the VMs. You will need to edit this file to provide appropriate IP addresses and other VM configuration data (see "Instructions" below).

* **user-data**: This file is used to customize the CoreOS instances when they are instantiated by Vagrant. You will need to edit this file to provide an appropriate etcd discovery URL (see "Instructions" below).

## Instructions

These instructions assume you've already installed VMware Fusion, Vagrant, and the Vagrant VMware plugin. Please refer to the documentation for those products for more information on installation or configuration.

1. Use `vagrant box add` to install the CoreOS Vagrant box for the vmware_fusion provider. At the time of writing, the correct link to install was [http://stable.release.core-os.net/amd64-usr/current/coreos_production_vagrant_vmware_fusion.json](http://stable.release.core-os.net/amd64-usr/current/coreos_production_vagrant_vmware_fusion.json). Use a command like this:

	`vagrant box add http://stable.release.core-os.net/amd64-usr/current/coreos_production_vagrant_vmware_fusion.json`

2. Either clone this repository (using `git clone` with the GitHub HTTPS clone URL) or download and extract the ZIP file (using the "Download ZIP" link on GitHub).

3. Edit the `user-data` file in a text editor to insert a valid etcd discovery URL. You can obtain a new discovery URL by visiting [https://discovery.etcd.io/new](https://discovery.etcd.io/new) and using the full URL returned in the browser. The `user-data` file is commented on where this information needs to be inserted.

4. Edit the `servers.yml` to provide the details on the VMs that Vagrant should create. The `Vagrantfile` expects six values for each VM: `name` (the user-friendly name of the VM; will also be used as the hostname inside the VM), `box` (use "coreos-stable", which corresponds to the box downloaded in step 1), `ram` (how much RAM should be assigned to the VM), `vcpu` (how many vCPUs should be assigned to the VM), `priv_ip` (a static IP address assignment from a private IP address range), and `pub_ip` (a static IP address assignment from a public IP address).

	Ensure that the values you assign to `priv_ip` and `pub_ip` will allow the resulting VMs to have Internet connectivity. Without Internet connectivity, the etcd cluster setup will fail. Remember that Vagrant always assigns VMs to a private network, so this configuration will result in VMs with 3 network interfaces. You **cannot** use DHCP for the additional network interfaces; addresses need to be assigned statically via `servers.yml` and the `Vagrantfile`.

5. After you've edited both `user-data` (to provide the correct etcd discovery URL) and `servers.yml` (to provide the correct values for the VMs), you can use `vagrant up` in the directory where these files are stored to bring up the VMs.

6. Once Vagrant has finished bringing up the VMs, simply use `vagrant ssh <name>` (where `<name>` is the value assigned to the VM from `servers.yml`) to connect to one of the CoreOS systems. No password should be required; it should use the default (insecure) SSH key. You can use the following commands to verify that everything is working correctly:

	`cat /etc/environment` (the values should reflect the values from `servers.yml`)

	`systemctl status etcd` (should show that etcd is running and active)

	`netstat -tan | grep LISTEN` (should show ports 4001 and 7001 listening)

	`fleetctl list-machines` (should list all the VMs you told Vagrant to create via `servers.yml`)

Enjoy!