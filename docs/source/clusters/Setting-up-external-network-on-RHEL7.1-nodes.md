## Setting Up External Network
On RHEL 7.1 nodes 

### Configuration
**Hardware iface ifcfg script** (`/etc/sysconfig/network-scripts/ifcfg-enp130s0f0`)
```shell
BOOTPROTO="dhcp"
DEVICE="enp130s0f0"
HWADDR="90:e2:ba:8e:bd:64"
ONBOOT=yes
PEERDNS=no
DEFROUTE=no
PEERROUTES=no
```
**Virtual tagged iface ifcfg script** (`/etc/sysconfig/network-scripts/ifcfg-enp130s0f0.125`)
```shell
VLAN=yes
TYPE=Vlan
BOOTPROTO=static
DEVICE="enp130s0f0.125"
NAME="enp130s0f0.125"
ONBOOT=yes
MTU=9000
IPADDR=129.10.3.xx
NETMASK=255.255.255.0
GATEWAY=129.10.3.1
DNS1=8.8.8.8
```
**OSP Repo** (`/etc/yum.repos.d/osp.repo`)
```shell
[osp]
name=osp
baseurl= ftp://partners.redhat.com/b5d52ebbb756856c8e7e6f44880b4741/OpenStack/7.0-RHEL-7/2015-06-24.1/RH7-RHOS-7.0/x86_64/os/
gpgcheck=0
enabled=1
```
**EPEL Repo** (`/etc/yum.repos.d/epel.repo`)
```shell
[epel]
name=epel
baseurl=http://dl.fedoraproject.org/pub/epel/7/x86_64/
gpgcheck=0
enabled=1
```

### Subscribe to RHN
```shell
# subscription-manager register
# subscription-manager attach --auto
# subscription-manager list
```
