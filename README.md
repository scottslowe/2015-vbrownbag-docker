# Support files for "Docker and Friends"

This repository contains a variety of support files from the #vBrownBag presentation on Docker and related tools (titled "Docker and Friends") given on 28 January 2015.

## Contents

* **README.md**: The file you're reading right now.

* **vagrant-coreos**: Configuration files to spin up a CoreOS cluster running etcd. See the README.md file in this directory for more information.

* **coreos-cloud-config-openstack.yml**: A cloud-config file to be used when deploying CoreOS on an OpenStack cloud. This cloud-config file can be supplied as "user-data". If you want to spin up a working etcd cluster, you'll need to edit this file to supply a valid etcd discovery URL.

* **coreos-cluster-heat-template.yml**: An OpenStack Heat template to spin up a cluster of CoreOS instances running etcd. You'll need to edit this file to provide a valid etcd discovery URL as well as to supply the correct values for the Neutron network, the CoreOS Glance image, and the Neutron security group. (These values are most easily obtained using the `neutron` and `glance` CLI clients.)

* **docker-simple.yml**: A simple Heat template for deploying a Docker container to an already running instance that has the Docker daemon configured to listen on a network port.

* **nginx-??.service**: A set of systemd unit files that can be used with `fleetctl` to deploy 3 instances of Nginx across a cluster of CoreOS systems running etcd.

* **presentation.md**: The Markdown source for the #vBrownBag presentation.

* **presentation.pdf**: The formatted presentation.

* **sa-nginx.service**: A systemd unit file to run a Docker container on a CoreOS system.

## License

This material is licensed under the MIT License.