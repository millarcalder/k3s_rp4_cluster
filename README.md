# civilstonks-elk

This project contains ansible roles I use for setting up each Raspberry Pi 4 in my Kubernetes cluster.

## Setup a Raspberry Pi

Currently this is only intended to be used with a raspberry pi 4 since it uses a arm64 processor.

1. setup SSH on the remote machine, see [this link](https://www.ssh.com/academy/ssh/copy-id) for instructions
2. setup a inventory file
3. run the `setup_raspberry_pi` ansible playbook, e.g. `ansible-playbook playbook.yml -i production.yml --ask-become-pass`

### Inventory File

When setting up a Raspberry Pi the ansible playbook will need to remotely execute commands on the machine, so you will need to setup an inventory file with some details about the machine.

#### Master Node

```
[webservers]
rp01 ansible_connection=ssh ansible_host=192.168.1.1 hostname=pimaster ansible_user=ubuntu server_node=True
```

#### Worker Node

```
[webservers]
rp01 ansible_connection=ssh ansible_host=192.168.1.1 hostname=piagent1 ansible_user=ubuntu server_node=False k3s_url=... node_token=...
```
