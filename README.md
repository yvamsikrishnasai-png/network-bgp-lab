# network-bgp-lab
This project demonstrates a multi- Autonomous system routing lab set using BGP and OSPF protocols. the main objective is to configure and mamage routing policies,interior gateway protocols,and border gateway peerings across different network clods.
R1
R1#conf t
R1(config)#int g1/0
R1(config-if)#ip add 220.224.12.1 255.255.255.0
R1(config-if)#no shut
R1(config)#int g2/0
R1(config-if)#ip add 220.224.13.1 255.255.255.0
R1(config-if)#no shut
R1(config)#int lo0
R1(config-if)#ip add 1.1.1.1 255.255.255.0
R1(config-if)#exit

! OSPF Configuration (AS 120 Internal)
R1(config)#router ospf 10
R1(config-router)#network 220.224.12.0 0.0.0.255 area 0
R1(config-router)#network 220.224.13.0 0.0.0.255 area 0
R1(config-router)#network 1.1.1.1 0.0.0.0 area 0
R1(config-router)#exit

! BGP Configuration
R1(config)#router bgp 120
R1(config-router)#bgp router-id 1.1.1.1
R1(config-router)#neighbor 3.3.3.3 remote-as 120
R1(config-router)#neighbor 3.3.3.3 update-source lo0
R1(config-router)#neighbor 4.4.4.4 remote-as 120
R1(config-router)#neighbor 4.4.4.4 update-source lo0
R1(config-router)#network 1.1.1.1 mask 255.255.255.255
R1(config-router)#end
R2
R2#conf t
R2(config)#int g1/0
R2(config-if)#ip add 220.224.12.2 255.255.255.0
R2(config-if)#no shut
R2(config)#int e4/0
R2(config-if)#ip add 220.224.23.2 255.255.255.0
R2(config-if)#no shut
R2(config)#int g2/0
R2(config-if)#ip add 220.224.24.2 255.255.255.0
R2(config-if)#no shut
R2(config)#int lo0
R2(config-if)#ip add 3.3.3.3 255.255.255.0
R2(config-if)#exit

! OSPF Configuration
R2(config)#router ospf 10
R2(config-router)#network 220.224.12.0 0.0.0.255 area 0
R2(config-router)#network 220.224.23.0 0.0.0.255 area 0
R2(config-router)#network 3.3.3.3 0.0.0.0 area 0
R2(config-router)#exit

! BGP Configuration
R2(config)#router bgp 120
R2(config-router)#bgp router-id 3.3.3.3
R2(config-router)#neighbor 1.1.1.1 remote-as 120
R2(config-router)#neighbor 1.1.1.1 update-source lo0
R2(config-router)#neighbor 4.4.4.4 remote-as 120
R2(config-router)#neighbor 4.4.4.4 update-source lo0
R2(config-router)#neighbor 220.224.24.4 remote-as 130
R2(config-router)#end
R3
R3#conf t
R3(config)#int g2/1
R3(config-if)#ip add 220.224.13.3 255.255.255.0
R3(config-if)#no shut
R3(config)#int e4/1
R3(config-if)#ip add 220.224.23.3 255.255.255.0
R3(config-if)#no shut
R3(config)#int g1/0
R3(config-if)#ip add 220.224.36.3 255.255.255.0
R3(config-if)#no shut
R3(config)#int lo0
R3(config-if)#ip add 4.4.4.4 255.255.255.0
R3(config-if)#exit

! OSPF Configuration
R3(config)#router ospf 10
R3(config-router)#network 220.224.13.0 0.0.0.255 area 0
R3(config-router)#network 220.224.23.0 0.0.0.255 area 0
R3(config-router)#network 4.4.4.4 0.0.0.0 area 0
R3(config-router)#exit

! BGP Configuration
R3(config)#router bgp 120
R3(config-router)#bgp router-id 4.4.4.4
R3(config-router)#neighbor 1.1.1.1 remote-as 120
R3(config-router)#neighbor 1.1.1.1 update-source lo0
R3(config-router)#neighbor 3.3.3.3 remote-as 120
R3(config-router)#neighbor 3.3.3.3 update-source lo0
R3(config-router)#neighbor 220.224.36.6 remote-as 150
R3(config-router)#end
R4
R4#conf t
R4(config)#int g1/0
R4(config-if)#ip add 220.224.24.4 255.255.255.0
R4(config-if)#no shut
R4(config)#int e4/1
R4(config-if)#ip add 220.224.45.4 255.255.255.0
R4(config-if)#no shut
R4(config)#int lo0
R4(config-if)#ip add 5.5.5.5 255.255.255.0
R4(config-if)#exit

R4(config)#router bgp 130
R4(config-router)#bgp router-id 5.5.5.5
R4(config-router)#network 5.5.5.5 mask 255.255.255.255
R4(config-router)#neighbor 220.224.24.2 remote-as 120
R4(config-router)#neighbor 220.224.45.5 remote-as 140
R4(config-router)#end
R5
R5#conf t
R5(config)#int e4/2
R5(config-if)#ip add 220.224.45.5 255.255.255.0
R5(config-if)#no shut
R5(config)#int e4/3
R5(config-if)#ip add 220.224.56.5 255.255.255.0
R5(config-if)#no shut
R5(config)#int lo0
R5(config-if)#ip add 6.6.6.6 255.255.255.0
R5(config-if)#exit

R5(config)#router bgp 140
R5(config-router)#bgp router-id 6.6.6.6
R5(config-router)#network 6.6.6.6 mask 255.255.255.255
R5(config-router)#neighbor 220.224.45.4 remote-as 130
R5(config-router)#neighbor 220.224.56.6 remote-as 150
R5(config-router)#end
R6
R6#conf t
R6(config)#int g1/0
R6(config-if)#ip add 220.224.36.6 255.255.255.0
R6(config-if)#no shut
R6(config)#int e4/3
R6(config-if)#ip add 220.224.56.6 255.255.255.0
R6(config-if)#no shut
R6(config)#int lo0
R6(config-if)#ip add 7.7.7.7 255.255.255.0
R6(config-if)#exit

R6(config)#router bgp 150
R6(config-router)#bgp router-id 7.7.7.7
R6(config-router)#network 7.7.7.7 mask 255.255.255.255
R6(config-router)#neighbor 220.224.36.3 remote-as 120
R6(config-router)#neighbor 220.224.56.5 remote-as 140
R6(config-router)#end
