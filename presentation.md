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

---
# **Container-optimized operating systems**

Following the rise of Docker, a number of _container-optimized operating systems_ have emerged. They include:

* CoreOS Linux
* Project Atomic
* Snappy Ubuntu Core

^ "Container-optimized" means slimmer than normal Linux distributions, typically Docker is pre-installed, and may have additional container-specific tools/features

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
# **Using Docker with OpenStack Heat**

---
# **Using Docker with fleet**

---
# [fit] **Q&A**

---
# **Thank you!**

Blog: http://blog.scottlowe.org
Twitter: @scott_lowe
GitHub: https://github.com/lowescott/
IRC: slowe on Freenode
Life: Colossians 3:17
