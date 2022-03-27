# Setup Raspberry Pi 4

## Operating system

[ubuntu server 20.04](https://releases.ubuntu.com/20.04/)

### SSH Key

You will need to setup a SSH key for ansible.

https://www.ssh.com/academy/ssh/copy-id

### PoE+ Hat

You need to do some custom configuration for this since we aren't using raspian os, add this config to `/boot/firmware/usercfg.txt`

```
dtoverlay=rpi-poe
dtparam=poe_fan_temp0=10000,poe_fan_temp0_hyst=1000
dtparam=poe_fan_temp1=55000,poe_fan_temp1_hyst=5000
dtparam=poe_fan_temp2=60000,poe_fan_temp2_hyst=5000
dtparam=poe_fan_temp3=65000,poe_fan_temp3_hyst=5000
```

#### Links

https://forums.raspberrypi.com/viewtopic.php?t=313098

### cgroup memory

You need to enable cgroup memory. Append the following to `/boot/firmware/cmdline.txt`.

```
cgroup_enable=cpuset cgroup_enable=memory cgroup_memory=1
```

#### Links

https://microk8s.io/docs/install-alternatives#heading--arm
https://manpages.ubuntu.com/manpages/focal/man7/cgroups.7.html
https://askubuntu.com/questions/1237813/enabling-memory-cgroup-in-ubuntu-20-04
https://askubuntu.com/questions/1189480/raspberry-pi-4-ubuntu-19-10-cannot-enable-cgroup-memory-at-boostrap
