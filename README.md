# Raspberry Pi Kubernetes Cluster

This project contains ansible roles that setup a [K3S Kubernetes cluster](https://k3s.io/) on some Raspberry Pi 4's that I have for some fun :smile:

Currently this is only intended to be used with a Raspberry Pi 4 running Ubuntu Server 22.10.

## Setup a Raspberry Pi 4

1. istall [Ubuntu Server 22.10](https://releases.ubuntu.com/22.10/)
1. setup SSH key on the remote machine, see [this link](https://www.ssh.com/academy/ssh/copy-id) for instructions
2. setup an inventory file in `./inventory/*` (see below for details)
3. run the `setup_raspberry_pi` ansible playbook, e.g. `ansible-playbook setup_raspberry_pi.yml -i production.yml --ask-become-pass`
4. Configure kubectl access to your remote cluster (https://docs.k3s.io/cluster-access)

### Inventory File

The ansible playbook will execute commands on the target remote machine, so you will need to setup an inventory file with some details about the machine.

#### Master Node

```
[webservers]
rp01 ansible_connection=ssh ansible_host=192.168.1.1 hostname=pimaster ansible_user=ubuntu server_node=True
```

#### Worker Node

```
[webservers]
rp01 ansible_connection=ssh ansible_host=192.168.1.2 hostname=piagent1 ansible_user=ubuntu server_node=False k3s_url=... node_token=...
```

`k3s_url` - the url for the Kubernetes cluster, e.g. http://192.168.1.1:6443/  
`node_token` - the value to use for `node_token` is stored at `/var/lib/rancher/k3s/server/node-token` on your server node

## Useful Links

[K3S Quickstart](https://docs.k3s.io/quick-start)
