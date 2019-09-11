# Ansible scripts for Sirius

### Prerequirements:
1. Debian 9.x or above
2. Ansible installed 


### Setup node with minimal configuration


**Install Ansible**

1. ```echo 'deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main' >> /etc/apt/sources.list```
2. ```apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367```
3. ```apt-get update```
4. ```apt-get install -y ansible sshpass```

**Add ansible user with sudo and with ssh access**

**Install sudo** ```apt-get install -y sudo```

**Edit** ```/etc/sudoers``` file: ```echo 'ansible ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers```

