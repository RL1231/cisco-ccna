# CCNA - STP & Etherchannels
STP configuration using Rapid PVST+ and Etherchannels

## Process
- Create vlans on each switch.
- Trunk connecting ports to each switch
- Configure sub-interfaces on router
- Configure Rapid PVST+ and Etherchannel between SW1 and SW2

## Command Example
(Refer to 01-CCNA and 02-CCNA to see similar inter-vlan configuration)

RAPID PVST+ CONFIGURATION:
SW1(config)#spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree bpduguard default
SW1(config)#spanning-tree vlan 10 root primary
SW1(config)#spanning-tree vlan 20 root secondary

SW2(config)#spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree bpduguard default 
SW2(config)#spanning-tree vlan 20 root primary
SW2(config)#spanning-tree vlan 30 root secondary

SW3(config)#spanning-tree mode rapid-pvst
spanning-tree portfast default
spanning-tree bpduguard default
SW3(config)#spanning-tree vlan 30 root primary
SW3(config)#spanning-tree vlan 10 root secondary

ETHERCHANNEL CONFIGURATION (SW1 & SW2):
SW1(config)# int range int e0/1-2
SW1(config-if-range)# channel-group 1 mode active
SW1(config-if-range)# switchport trunk encapsulation dot1q
SW1(config-if-range)# switchport mode trunk
SW1(config-if-range)# switchport trunk allowed vlan 10,20,30
SW1(config)#int Po1
SW1(config-if)# switchport trunk encapsulation dot1q
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport trunk allowed vlan 10,20,30


