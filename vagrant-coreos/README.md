# Building a CoreOS etcd Cluster with Vagrant

These files are intended to allow users to use Vagrant to quickly spin up a cluster of CoreOS systems running etcd.

## Files

* **README.md**: This file that you're reading now.

* **Vagrantfile**: This file is used by Vagrant to spin up the virtual machines.

* **servers.yml**: This YAML file contains a list of VM definitions. It is referenced by `Vagrantfile` when Vagrant instantiates the virtual machines.

* **user-data**: This file is used to customize the CoreOS instances when they are instantiated by Vagrant.

## Instructions

1. 