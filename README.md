# Ansible scripts for Sirius

### Prerequirements:
1. Debian 9 stretch
2. Ansible installed 
3. Setup Valid Hostname ```hostnamectl``` command and editing ```/etc/hohst``` file


### Setup node with minimal configuration

**Install Ansible**

1. ```echo 'deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main' >> /etc/apt/sources.list```
2. ```apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367```
3. ```apt-get update```
4. ```apt-get install -y ansible sshpass```

**Add ansible user with sudo and with ssh access**

**Install sudo** ```apt-get install -y sudo```

**Edit** ```/etc/sudoers``` file: ```echo 'ansible ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers```


### Docker provisioning
1. Install ansible role: ```ansible-galaxy install nickjj.docker```
2. Usage: ```ansible-playbook docker-playbook.yml```

### Install KAFKA Cluster

1. Clone repo ```git clone https://github.com/Sirius-social/ansible-playbook-kafka.git```
2. ```cd ansible-playbook-kafka```
3. ```ansible-playbook -i <sirius-inventory-file> kafka_install_playbook.yml```
4. ```ansible-playbook -i <sirius-inventory-file> control_center_setup_playbook.yml```

### Prepare KAFKA Cluster Control Center

[https://docs.confluent.io/3.3.0/control-center/docs/quickstart.html](https://docs.confluent.io/3.3.0/control-center/docs/quickstart.html)

1. On admin machine navigate ```cd /etc/confluent-control-center```
2. Edit ```control-center-production.properties``` file: Set actual value for parameter ```confluent.controlcenter.rest.listeners```
3. Start Control Center ```/usr/bin/control-center-start /etc/confluent-control-center/control-center-production.properties```
4. Wait for 30-60 sec

### Setup Postgres Cluster: Patroni + HAProxy

1. Install postgres: ```ansible-playbook postgres-playbook.yml```
2. Install Patroni (zookeeper must be runned): ```ansible-playbook patroni-playbook.yml```
3. Install HAProxy: ```ansible-playbook -e "patroni_replication_password=<replicator_pass>" -e "<superuser_pass>" patroni-playbook.yml```
4. Install POWA Monitorinh tool: 

### Setup Gluster support

1. ```ansible-galaxy install "geerlingguy.glusterfs```
2. ```ansible-play  ansible-playbook gluster_playbook.yml```
