+++
title = "Vps Config"
date = 2022-11-20T19:18:00-05:00
lastmod = 2022-11-20T19:18:00-05:00
tags = ["Config","VPS"]
categories = ["Linux"]
imgs = []
cover = ""  # image show on top
readingTime = true  # show reading time after article date
toc = true
comments = false
justify = false  # text-align: justify;
single = false  # display as a single page, hide navigation on bottom, like as about page.
license = ""  # CC License
+++


A server configuration is a set of instructions that tells a computer how to operate. The instructions can include the type of hardware to use, the software to install, and the settings to use. A server configuration can be used to set up a new computer, or to change the settings on an existing computer.
Here is the configuration I usually use for my fresh new sever:

<!--more-->
# Host
1. declare hosts 

Code

    /etc/hosts
Exemple:

	173.249.31.236 node2
	144.91.95.252 node1

1. change hostname

Edit hostname files

    vim /etc/hostname
    vim /etc/hosts


# Change SSH
1. Open the /etc/ssh/sshd_config file
2. Locate the following line:

        Port 7823
4. Restart the SSH service using the appropriate command for your Linux distribution:

        service ssh restart
# Docker
      $ apt install docker docker-compose -y
      $ sudo systemctl start docker
      $ sudo systemctl enable docker
      $ sudo usermod -aG docker $USER
      $ sudo newgrp docker
      $ sudo usermod -aG docker [non-root user]

# Swarm
        docker swarm init --advertise-addr 144.91.95.252

# Gluster 
1. install in all nodes:

        sudo apt-get install software-properties-common -y
        sudo apt-get update

        sudo apt install glusterfs-server -y

        sudo systemctl start glusterd
        sudo systemctl enable glusterd

1. generate ssh

        ssh-keygen -t rsa

2. probe "master only"

        gluster peer probe node2;
        gluster pool list


1. create volume "all machines"
   
        sudo mkdir -p /gluster/swarm

"master only"

        sudo gluster volume create swarm-gfs replica 2 node1:/gluster/swarm node2:/gluster/swarm force

1. start volume 
        
        sudo gluster volume start swarm-gfs

        echo 'localhost:/swarm-gfs /mnt glusterfs defaults,_netdev,backupvolfile-server=localhost 0 0' >> /etc/fstab
        mount.glusterfs localhost:/swarm-gfs /mnt
        chown -R root:docker /mnt

# Portainer 
ON manager
        
        curl -L https://downloads.portainer.io/portainer-agent-stack.yml -o portainer-agent-stack.yml
        
        docker stack deploy         --compose-file=portainer-agent-stack.yml portainer
