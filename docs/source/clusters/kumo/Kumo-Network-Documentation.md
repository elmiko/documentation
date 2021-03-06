## Kumo Network Documentation

Since we have merged the networks/VLANs in Kumo and Kaizen, all networking related upates should go here: https://moc-documents.readthedocs.io/en/latest/clusters/kaizen2/Kaizen-2.html?#public-bu-vlan-105


### IP addresses

**Public (via CSAIL)**
 -  128.31.28.11        Recursive DNS server

**Public (via BU VLAN 105)**

This VLAN is now documented here: https://moc-documents.readthedocs.io/en/latest/clusters/kaizen2/Kaizen-2.html?#public-bu-vlan-105


### VLANs
 -  0010(10G)      connection to engage1 Public/Csail, dhcp
 -  0105(10G)      Public/BU - infrastructure, 192.12.185.0/24
 -  200(10G)       Internet Access via NATing gateway. HIL admin network.
 -  3699(10G)      Foreman provision 10G, 172.16.0.0/22
 -  172.16.0.\*
     -  001     Foreman
     -  010-100 Foreman dhcp during initial install only.
     -  251     kumo-centos-repos
     -  252     kumo-repos
     -  253     kumo-s
     -  254     kumo-e
     -  172.16.1.0 - 172.16.1.255  Foreman static assignments for hosts
     -  172.16.2.0 - 172.16.3.254  Available
 -  3700(10G)      ceph client network, 192.168.16.0/22
 -  Ceph  hosts       192.168.16.0/24
     -  Mon/OSD       1,2,3
     -  kumo-cephmanager 255
     -  kumo-e           254
     -  kumo-s           253
     -  kumo-foreman     252
     -  kumo-rgw1        251
     -  kumo-rgw2        250
 -  Openstack  hosts  192.168.17.0/24
 -  BMI  192.168.18.0/24
     -  Kumo-Storage  192.168.18.113
     -  DHCP         192.168.19.0/24
 -  3701(10G)      ceph cluster network, 192.168.20.0/22
 -  3702(10G)      openstack private net, 192.168.32.0/22
 -  3703(10G)      undercloud provision, 192.168.24.0/24
 -  3704(10G)      openstack tenant net, 192.168.12.0/22
 -  3800(10G)      Shared VLAN with engage1 and kaizen
 -  3803(10G)      Public/Csail - floating IPs and infrastructure devices with direct connection to Kai/E1, 128.31.28.0/24
 -  4050(10G)      connection to engage1 ceph public
 -  4052(10G)      connection to engage1 openstack private
 -  3040(1G)      connection to Eng1 IPMI ,10.10.10.0/24
 -  4013(1G)      ipmi, 10.1.10.0/23
 -  4014(1G)      provisioning/foremnan, 10.13.96.0/22

## IPMI IPs

 -  10.1.11.1      Cisco Catalyst Switch, see bitwarden Kumo Cisco Catalyst password
 -  10.1.11.2      Cisco Nexus Switch, see bitwarden Kumo Nexus passord
 -  10.1.11.3      Kumo emergency managing port
 -  10.1.11.4      Kumo services managing port
 -  10.1.11.5      Dell M1000e CMC, see bitwarden Dell M1000e CMC password
 -  10.1.11.6      Kumo-storage1, Dell R720/MD1200, see bitwarden Dell R720/MD1200 password
 -  10.1.11.7      kumo-ceph01
 -  10.1.11.8      kumo-ceph02
 -  10.1.11.9      kumo-ceph03
 -  10.1.11.10     kumo-cacti
 -  10.1.11.11     Kumo emergency IPMI access, see bitwarden Kumo Emergency IPMI password
 -  10.1.11.12     Kumo services IPMI access, see bitwarden Kumo Services IPMI password
 -  10.1.11.14     Kumo hil master (non-keysone; VM)
 -  10.1.11.15     Mellanox M405EX (mlx001), see bitwarden Kumo Mellanox M405EX password
 -  10.1.11.16     Dell-16 (Current Ironic Controller)
 -  10.1.11.17     kumo-ipmi-gw managing port
 -  10.1.11.19     MaaS controller (to manage kumo hosts)
 -  10.1.10.1-16      Dell Blades
 -  10.1.10.2      Dell Blade 2
 -  10.1.10.3      Dell Blade 3
 -  10.1.10.12      Dell Blade 12
 -  10.1.10.13      Dell Blade 14
 -  10.1.10.14      Dell Blade 16
 -  10.1.10.16      Dell Blades
 -  10.0.23.100+x   Dell Blade X (Rest of the dell blades that are on kaizen IPMI network now)

### Provisioning network static IPs
*check Foreman for current hosts*
 -  10.13.96.1        kumo-foreman
 -  10.19.97.47       kumo-hil

### VMs on Kumo Storage01 (private-isolated network)
 -  interface Ethernet1/17
     -  switchport mode trunk
     -  switchport trunk allowed vlan 105,200,300-400,500-520,3700
 -  It's interface (enp67s0f1np1) is connected to Port Ethernet 1/17 to nexus
switch.
 -  It's interface (enp67s0f0np0) is connected to Port Ethernet 1/21 to nexus
switch.
 -  192.168.100.141     Kumo-hil-client (also on public network)
 -  192.168.100.142     kumo-bmi-no-seccloud
 -  192.168.100.197     kumo-bmi-seccloud
 -  192.168.100.210     kumo-hil (HIL Master) (macvtap network; no connectivity)
 -  192.168.100.231     hil-headnode (for Han and Jim)

### HIL configuration notes
 -  HIL user:password = see bitwarden HIL admin password
 -  HIL is running on a VM on Kumo Storage 01.
 -  There are 2 projects for the 2 kumo environments. Don't mess with those, the
kumo environments are still alive. Talk to Naved/Rado before moving any nodes
out of those projects.
 -  For root pass of HIL and BMI, see bitwarden HIL root password

### kumo-hil-client
 -  Runs the HIL Client
 -  Acts as the public gateway for HIL services (and BMI)

### Port mapping
 -  dell-X's 2 ports, em1 and em2, are connected to Ethernet1/X and Ethernet1/(X+24)
respectively. Eg; dell-10's ports are connected to Ethernet1/10 and Ethernet1/34.

### BMI Setup
 -  Login details for the ubuntu image in `naved` project: 
 see bitwarden Ubuntu Image root and Ubuntu Image BMI password
     -  root login over ssh is disabled by default.
 -  There are 2 BMI setups in Kumo. Below is the information about the two

**kumo-bmi-no-seccloud** VM running on kumo-storage01.
 -  Storage Network IP - 192.168.18.76 (/22)
 -  HIL Network IP - 192.168.100.142

**kumo-bmi-seccloud** VM running on kumo-storage01.
 -  Storage Network IP - 192.168.18.117 (/22)
 -  HIL Network IP - 192.168.100.197
