# CCNA - OSPF (Single Area)
OSPFv2 configuration of a single area

## Process
- Determine roles of each backbone router
- Configure router to WAN as ASBR 
- Configure passive interfaces (including loopback interface)
- Configure point-to-point OSPF segments

## Command Example
BR(config)# router ospf 1
BR(config)# network 172.1.1.1 0.0.0.0 area 0
BR(config)# network 192.168.0.0 0.0.0.3 area 0
BR(config)# network 192.168.1.0 0.0.0.255 area 0
BR(config)# network 192.168.2.0 0.0.0.255 area 0
BR(config)# network 192.168.3.0 0.0.0.255 area 0
BR(config)# passive-interface l0
BR(config)# passive-interface e0/3
BR(config)# int e0/0
BR(config-f)# ip ospf network  point-to-point

ABR1(config)# router ospf 1
ABR1(config)# network 172.2.2.2 0.0.0.0 area 0
ABR1(config)# network 192.168.1.0 0.0.0.255 area 0
ABR1(config)# passive-interface l0

ABR2(config)# router ospf 1
ABR2(config)# network 172.3.3.3 0.0.0.0 area 0
ABR2(config)# network 192.168.2.0 0.0.0.255 area 0
ABR2(config)# passive-interface l0

ASBR(config)# router ospf 1
ASBR(config)# default-information originate
ASBR(config)# network 172.4.4.4 0.0.0.0 area 0
ASBR(config)# network 192.168.0.0 0.0.0.3 area 0
ASBR(config)# passive-interface l0
ASBR(config)# int e0/0
ASBR(config-f)# ip ospf network  point-to-point

