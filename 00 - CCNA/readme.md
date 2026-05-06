# CCNA - Subnetting
A subnet 192.168.1.0/24 divided into three subnets for demonstration purposes

## Process
I have 254 addresses. I can make no less than 4 subnets with 62 address each for at least 3 subnets.

- Subnet 1: 192.168.1.0/26   - 6 host bits (64 - 2)
- Subnet 2: 192.168.1.64/26  - 6 host bits (64 - 2) 
- Subnet 3: 192.168.1.128/30 - 2 host bits (4 - 2) (point-to-point)
- Extra 122 (124 - 2) addresses

## Command Example
R1(config)# int e0/2
R1(config-if)# ip address 192.168.1.1 255.255.255.192
R1(config-if)# no shutdown

R1(config)# int e/01
R1(config-if)# ip address 192.168.1.129 255.255.255.252
R1(config-if)# no shutdown

R2(config)# int e0/0
R2(config-if)# ip address 192.168.1.65 255.255.255.192
R2(config-if)# no shutdown

R2(config)# int e0/1
R2(config-if)# ip address 192.168.1.30 255.255.255.252
R2(config-if)# no shutdown