# **Docker and Friends**

## 

---
# **What we'll review tonight**

* Container-optimized operating systems
* Using Docker with CoreOS
* Using Docker with OpenStack Heat
* Using Docker with fleet

---
# **Resources for following along**

The [GitHub repo for this session](http://github.com/lowescott/2015-vbrownbag-docker) contains some useful resources for following along:

* Sample systemd unit files for use both with and without fleet
* Sample cloud-config file for deploying CoreOS on both OpenStack and Vagrant
* Sample OpenStack Heat templates for deploying a CoreOS cluster as well as for deploying Docker containers
* This presentation's source

---
# **Container-optimized operating systems**

Following the rise of Docker, a number of _container-optimized operating systems_ have emerged. They include:

* CoreOS Linux
* Project Atomic
* Snappy Ubuntu Core

^ "Container-optimized" means slimmer than normal Linux distributions, typically Docker is pre-installed, and may have additional container-specific tools/features (atomic/transactional updates, for example)
^ CoreOS is one of the early container-optimized OSes and offers additional features like etcd (distributed key-value store), fleet (primitive scheduler), and flannel (container networking)
^ Project Atomic is backed by Red Hat and will create "Atomic" versions of Fedora, CentOS, and RHEL
^ Snappy Ubuntu is the most recent entry

---
# **Using Docker with CoreOS**

CoreOS (typically) uses systemd unit files to deploy Docker containers

```
[Unit]
Description=Nginx web front-end
After=docker.service
Requires=docker.service
 
[Service]
TimeoutStartSec=0
ExecStartPre=/usr/bin/docker pull nginx
ExecStart=/usr/bin/docker run --rm --name sa-nginx -p 80:80 nginx
ExecStop=/usr/bin/docker stop sa-nginx
```

---
# [fit] **Demo: Docker with CoreOS**

---
# **Using Docker with OpenStack Heat**

* Heat is an orchestration service for OpenStack
* Heat allows you to orchestrate the deployment/creation of networks, network topologies, instances, volumes
* Heat can orchestrate Docker containers if the Docker plug-in is installed

---
# **Docker+Heat Caveats**

* In Icehouse, Docker plugin was essentially broken (newer releases are better)
* Docker endpoints must be reachable from the Heat server
* Docker has to be configured to listen on a network port instead of only a local socket
* No intelligent placement of Docker containers

---
# [fit] **Demo: Docker with OpenStack Heat**

---
# **Using Docker with fleet**

* CoreOS offers a rudimentary scheduler called fleet
* Ties together systemd and etcd (distributed key-value store)
* Requires the presence of an etcd cluster
* Uses systemd unit files to deploy containers onto the cluster

---
# **Sample systemd unit file for fleet**

```
[Unit]
Description=Nginx web front-end
After=docker.service
Requires=docker.service
 
[Service]
TimeoutStartSec=0
ExecStartPre=/usr/bin/docker pull nginx
ExecStart=/usr/bin/docker run --rm --name nginx-01 -p 80:80 nginx
ExecStop=/usr/bin/docker stop nginx-01

[X-Fleet]
Conflicts=nginx-*.service
```

---
# [fit]  **Demo: Docker with fleet**

---
# [fit] **Q&A**

---
# **More resources: OpenStack Heat**

* An Introduction to OpenStack Heat - [http://blog.scottlowe.org/2014/05/01/an-introduction-to-openstack-heat/](http://blog.scottlowe.org/2014/05/01/an-introduction-to-openstack-heat/)
* Another Look at an OpenStack Heat Template - [http://blog.scottlowe.org/2014/05/02/another-look-at-an-openstack-heat-template/](http://blog.scottlowe.org/2014/05/02/another-look-at-an-openstack-heat-template/)
* Deploying CoreOS on OpenStack Using Heat - [http://blog.scottlowe.org/2014/08/13/deploying-coreos-on-openstack-using-heat/](http://blog.scottlowe.org/2014/08/13/deploying-coreos-on-openstack-using-heat/)

---
# **More resources: CoreOS, etcd, Fleet**

* CoreOS Continued: etcd - [http://blog.scottlowe.org/2014/08/18/coreos-continued-etcd/](http://blog.scottlowe.org/2014/08/18/coreos-continued-etcd/)
* CoreOS Continued: Fleet and Docker - [http://blog.scottlowe.org/2014/08/20/coreos-continued-fleet-and-docker/](http://blog.scottlowe.org/2014/08/20/coreos-continued-fleet-and-docker/)

---
# **More resources: Heat+Docker**

* Installing the Docker Plugin for Heat - [http://blog.scottlowe.org/2014/07/31/installing-the-docker-plugin-for-heat/](http://blog.scottlowe.org/2014/07/31/installing-the-docker-plugin-for-heat/)
* A Heat Template for Docker Containers - [http://blog.scottlowe.org/2014/08/22/a-heat-template-for-docker-containers/](http://blog.scottlowe.org/2014/08/22/a-heat-template-for-docker-containers/)

---
# **Thank you!**

Blog: [http://blog.scottlowe.org](http://blog.scottlowe.org)
Twitter: [@scott_lowe](https://twitter.com/scott_lowe)
GitHub: [https://github.com/lowescott/](https://github.com/lowescott/)
IRC: slowe (on Freenode)
Life: Colossians 3:17
