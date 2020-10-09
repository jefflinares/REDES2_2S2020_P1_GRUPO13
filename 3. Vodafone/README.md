# Red de telefonica

Vodafone le pide que configure una red con una topología Hub and Spoke, y que se
configure mediante un protocolo de enrutamiento OSPF (7 routers mínimo, 14 hosts,
distribuidos de la manera que usted considere prudente.).

---------------------------------------ROUTER 1
enable

conf t

interface fastethernet 0/0

ip address 192.168.1.1 255.255.255.0

no shut

exit

interface serial 2/0

ip address 10.10.10.2 255.255.255.252

no shut

exit

router ospf 1

network 192.168.1.0 0.0.0.255 area 1

network 10.10.10.0 0.0.0.3 area 1

exit

exit


show ip route ospf

---------------------------------------ROUTER 2
enable
conf t
interface fastethernet 0/0
ip address 192.168.2.1 255.255.255.0
no shut
exit
interface serial 2/0
shut
ip address 10.10.10.6 255.255.255.252
no shut
exit
router ospf 1
network 192.168.2.0 0.0.0.255 area 1
network 10.10.10.4 0.0.0.3 area 1
exit
exit

show ip route ospf

---------------------------------------ROUTER 3
enable
conf t
interface fastethernet 0/0
ip address 192.168.3.1 255.255.255.0
no shut
exit
interface serial 2/0
shut
ip address 10.10.10.10 255.255.255.252
no shut
exit
router ospf 1
network 192.168.3.0 0.0.0.255 area 1
network 10.10.10.8 0.0.0.3 area 1
exit
exit

show ip route ospf

---------------------------------------ROUTER 4
enable
conf t
interface fastethernet 0/0
ip address 192.168.4.1 255.255.255.0
no shut
exit
interface serial 2/0
shut
ip address 10.10.10.14 255.255.255.252
no shut
exit
router ospf 1
network 192.168.4.0 0.0.0.255 area 1
network 10.10.10.12 0.0.0.3 area 1
exit
exit

show ip route ospf

---------------------------------------ROUTER 5
enable
conf t
interface fastethernet 0/0
ip address 192.168.5.1 255.255.255.0
no shut
exit
interface serial 2/0
shut
ip address 10.10.10.18 255.255.255.252
no shut
exit
router ospf 1
network 192.168.5.0 0.0.0.255 area 1
network 10.10.10.16 0.0.0.3 area 1
exit
exit

show ip route ospf

---------------------------------------ROUTER 6
enable
conf t
interface fastethernet 0/0
ip address 192.168.6.1 255.255.255.0
no shut
exit
interface serial 2/0
shut
ip address 10.10.10.22 255.255.255.252
no shut
exit
router ospf 1
network 192.168.6.0 0.0.0.255 area 1
network 10.10.10.20 0.0.0.3 area 1
exit
exit

show ip route ospf

---------------------------------------ROUTER 7
enable
conf t
interface fastethernet 0/0
ip address 192.168.7.1 255.255.255.0
no shut
exit
interface serial 2/0
shut
ip address 10.10.10.26 255.255.255.252
no shut
exit
router ospf 1
network 192.168.7.0 0.0.0.255 area 1
network 10.10.10.24 0.0.0.3 area 1
exit
exit

show ip route ospf

---------------------------------------ROUTER 0
enable
conf t
interface serial 1/0
ip address 10.10.10.1 255.255.255.252
no shut
interface serial 2/0
ip address 10.10.10.5 255.255.255.252
no shut
interface serial 3/0
ip address 10.10.10.9 255.255.255.252
no shut
interface serial 4/0
ip address 10.10.10.13 255.255.255.252
no shut
interface serial 5/0
ip address 10.10.10.17 255.255.255.252
no shut
interface serial 6/0
ip address 10.10.10.21 255.255.255.252
no shut
interface serial 7/0
ip address 10.10.10.25 255.255.255.252
no shut


router ospf 1
network 192.168.0.0 0.0.0.255 area 1
network 10.10.10.0 0.0.0.3 area 1
network 10.10.10.4 0.0.0.3 area 1
network 10.10.10.8 0.0.0.3 area 1
network 10.10.10.12 0.0.0.3 area 1
network 10.10.10.16 0.0.0.3 area 1
network 10.10.10.20 0.0.0.3 area 1
network 10.10.10.24 0.0.0.3 area 1
exit
exit

show ip route ospf
