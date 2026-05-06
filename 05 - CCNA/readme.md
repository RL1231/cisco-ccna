# CCNA - FHRP
HSRP redundancy configuration

## Process
- Create two router network with redundancy
- Configure router R1 as the Active router
- Configure router R2 as a Standby router
- Configure the virtual interface

## Command Example
R1(config)# int e0/0
R1(config-if)# ip address 192.168.1.2 255.255.255.0
R1(config-if)# standby 1 ip 192.168.1.1
R1(config-if)# standby 1 priority 110
R1(config-if)# standby preempt

R2(config)# int e0/0
R2(config-if)# ip address 192.168.1.3 255.255.255.0
R2(config-if)# standby 1 ip 192.168.1.1
R2(config-if)# standby 1 priority 100
R2(config-if)# standby preempt (optional)