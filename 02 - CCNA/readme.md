# CCNA - Inter-Vlan
Inter-vlan configuration using a layer 3 switch

## Process
- Create vlans on switch. One vlan per access port.
- Configure ip addresses on SVIs
- Configure DHCP relays to the router
- Configure DHCP on router

## Command Example
L3-SW1(config)# int range e0/0-4
L3-SW1(config-if-range)# switchport mode access
L3-SW1(config)# int e0/0
L3-SW1(config-if)# switchport access vlan 30
L3-SW1(config)# int e0/1
L3-SW1(config-if)# switchport access vlan 10
L3-SW1(config)# int e0/2
L3-SW1(config-if)# switchport access vlan 20
L3-SW1(config)# int e0/3
L3-SW1(config-if)# switchport access vlan 30

L3-SW1(config)# int vlan 10
L3-SW1(config-vlan)# ip address 192,168.1.1 255.255.255.0
L3-SW1(config-vlan)# ip helper-address 192.168.3.2 255.255.255.0
L3-SW1(config-vlan)# no shutdown
L3-SW1(config-vlan)# int vlan 20
L3-SW1(config-vlan)# ip address 192,168.2.1 255.255.255.0
L3-SW1(config-vlan)# ip helper-address 192.168.3.2 255.255.255.0
L3-SW1(config-vlan)# no shutdown
L3-SW1(config-vlan)# int vlan 30
L3-SW1(config-vlan)# ip address 192,168.3.1 255.255.255.0
L3-SW1(config-vlan)# ip helper-address 192.168.3.2 255.255.255.0
L3-SW1(config-vlan)# no shutdown

R1(config)# ip dhcp pool VLAN10
R1(config-dhcp)# network 192.168.1.0 255.255.255.0
R1(config-dhcp)# default-router 192.168.1.1
R1(config-dhcp)# dns-server 1.1.1.1 8.8.8.8

(Create DHCP pools for each vlan)





