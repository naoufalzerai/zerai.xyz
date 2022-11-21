+++
title = "Vps Config"
date = 2022-11-20T19:18:00-05:00
lastmod = 2022-11-20T19:18:00-05:00
tags = []
categories = []
imgs = []
cover = ""  # image show on top
readingTime = true  # show reading time after article date
toc = true
comments = false
justify = false  # text-align: justify;
single = false  # display as a single page, hide navigation on bottom, like as about page.
license = ""  # CC License
+++

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
      1. apt install docker docker-compose -y
      2. sudo systemctl start docker
      3. sudo systemctl enable docker
      4. sudo usermod -aG docker $USER
      5. sudo newgrp docker

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