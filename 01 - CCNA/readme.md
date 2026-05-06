# CCNA - ROAS
Router on a Stick configuration

## Process
- Create vlans on each switch. One vlan per access port.
- Trunk the two switches.
- Trunk  a switch to the router.
- Create sub interfaces on the router trunk port to switch
- Configure DHCP for each sub-interface

## Command Example
SW1(config)# vlan 10
SW1(config-vlan)# no shutdown
SW1(config)exit
SW1(config-vlan)# vlan 20
SW1(config-vlan)# no shutdown
SW1(config)exit
SW1(config-vlan)# vlan 99
SW1(config-vlan)# name NATIVE
SW1(config-vlan)# no shutdown   
SW1(config)exit

SW1(config)# int range e0/2-3
SW1(config-if-range)# switchport mode access
SW1(config)# int e0/2
SW1(config-if)# switchport access vlan 10
SW1(config)# int e0/3
SW1(config-if)# switchport access vlan 20

SW1(config)# int range e0/0-1
SW1(config-if-range)# switchport trunk encapsulation dot1q
SW1(config-if-range)# switchport mode trunk
SW1(config-if-range)# switchport trunk allowed vlan 10,20
SW1(config-if-range)# switchport trunk native vlan 99

(Same process for SW2)

R1(config)# int e0/1
R1(config-if)# no shutdown
R1(config-if)# int e0/1.10
R1(config-sub-if)# encapsulation dot1q 10
R1(config-sub-if)# ip address 192.168.1.1 255.255.255.0

(Same process for e0/1.20)

R1(config-if)# int e0/1.99
R1(config-sub-if)# encapsulation dot1q 99 native
R1(config-sub-if)# ip address 192.168.9.1 255.255.255.0

R1(config)# ip dhcp pool VLAN10
R1(config-dhcp)# network 192.168.1.0 255.255.255.0
R1(config-dhcp)# default-router 192.168.1.1
R1(config-dhcp)# dns-server 1.1.1.1 8.8.8.8

(Create DHCP pools for each sub-interface)





