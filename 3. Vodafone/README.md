# Red de telefonica

Vodafone le pide que configure una red con una topología Hub and Spoke, y que se
configure mediante un protocolo de enrutamiento OSPF (7 routers mínimo, 14 hosts,
distribuidos de la manera que usted considere prudente.).<br/>


##ROUTER 0
<br/>
enable<br/>
conf t<br/>
interface serial 1/0<br/>
ip address 10.10.10.1 255.255.255.252<br/>
no shut<br/><br/>
interface serial 2/0<br/>
ip address 10.10.10.5 255.255.255.252<br/>
no shut<br/><br/>
interface serial 3/0<br/>
ip address 10.10.10.9 255.255.255.252<br/>
no shut<br/><br/>
interface serial 4/0<br/>
ip address 10.10.10.13 255.255.255.252<br/>
no shut<br/><br/>
interface serial 5/0<br/>
ip address 10.10.10.17 255.255.255.252<br/>
no shut<br/><br/>
interface serial 6/0<br/>
ip address 10.10.10.21 255.255.255.252<br/>
no shut<br/><br/>
interface serial 7/0<br/>
ip address 10.10.10.25 255.255.255.252<br/>
no shut<br/><br/>
<br/>

router ospf 1<br/>
network 192.168.0.0 0.0.0.255 area 1<br/>
network 10.10.10.0 0.0.0.3 area 1<br/>
network 10.10.10.4 0.0.0.3 area 1<br/>
network 10.10.10.8 0.0.0.3 area 1<br/>
network 10.10.10.12 0.0.0.3 area 1<br/>
network 10.10.10.16 0.0.0.3 area 1<br/>
network 10.10.10.20 0.0.0.3 area 1<br/>
network 10.10.10.24 0.0.0.3 area 1<br/>
exit<br/>
exit<br/>

show ip route ospf<br/><br/>


##ROUTER 1
<br/>
enable<br/>
conf t<br/>
interface fastethernet 0/0<br/>
ip address 192.168.1.1 255.255.255.0<br/>
no shut<br/><br/>
exit<br/>
interface serial 2/0<br/>
ip address 10.10.10.2 255.255.255.252<br/>
no shut<br/><br/>
exit<br/>
router ospf 1<br/>
network 192.168.1.0 0.0.0.255 area 1<br/>
network 10.10.10.0 0.0.0.3 area 1<br/>
exit<br/>
exit<br/>

show ip route ospf<br/><br/>

##ROUTER 2
<br/>
enable<br/>
conf t<br/>
interface fastethernet 0/0<br/>
ip address 192.168.2.1 255.255.255.0<br/>
no shut<br/><br/>
exit<br/>
interface serial 2/0<br/>
shut<br/>
ip address 10.10.10.6 255.255.255.252<br/>
no shut<br/><br/>
exit<br/>
router ospf 1<br/>
network 192.168.2.0 0.0.0.255 area 1<br/>
network 10.10.10.4 0.0.0.3 area 1<br/>
exit<br/>
exit<br/>

show ip route ospf<br/><br/>

##ROUTER 3
<br/>
enable<br/>
conf t<br/>
interface fastethernet 0/0<br/>
ip address 192.168.3.1 255.255.255.0<br/>
no shut<br/><br/>
exit<br/>
interface serial 2/0<br/>
shut<br/>
ip address 10.10.10.10 255.255.255.252<br/>
no shut<br/><br/>
exit<br/>
router ospf 1<br/>
network 192.168.3.0 0.0.0.255 area 1<br/>
network 10.10.10.8 0.0.0.3 area 1<br/>
exit<br/>
exit<br/>

show ip route ospf<br/><br/>

##ROUTER 4
<br/>
enable<br/>
conf t<br/>
interface fastethernet 0/0<br/>
ip address 192.168.4.1 255.255.255.0<br/>
no shut<br/><br/>
exit<br/>
interface serial 2/0<br/>
shut<br/>
ip address 10.10.10.14 255.255.255.252<br/>
no shut<br/><br/>
exit<br/>
router ospf 1<br/>
network 192.168.4.0 0.0.0.255 area 1<br/>
network 10.10.10.12 0.0.0.3 area 1<br/>
exit<br/>
exit<br/>

show ip route ospf<br/><br/>

##ROUTER 5
<br/>
enable<br/>
conf t<br/>
interface fastethernet 0/0<br/>
ip address 192.168.5.1 255.255.255.0<br/>
no shut<br/><br/>
exit<br/>
interface serial 2/0<br/>
shut<br/>
ip address 10.10.10.18 255.255.255.252<br/>
no shut<br/><br/>
exit<br/>
router ospf 1<br/>
network 192.168.5.0 0.0.0.255 area 1<br/>
network 10.10.10.16 0.0.0.3 area 1<br/>
exit<br/>
exit<br/>

show ip route ospf<br/><br/>

##ROUTER 6
<br/>
enable<br/>
conf t<br/>
interface fastethernet 0/0<br/>
ip address 192.168.6.1 255.255.255.0<br/>
no shut<br/><br/>
exit<br/>
interface serial 2/0<br/>
shut<br/>
ip address 10.10.10.22 255.255.255.252<br/>
no shut<br/><br/>
exit<br/>
router ospf 1<br/>
network 192.168.6.0 0.0.0.255 area 1<br/>
network 10.10.10.20 0.0.0.3 area 1<br/>
exit<br/>
exit<br/>

show ip route ospf<br/><br/>

##ROUTER 7
<br/>
enable<br/>
conf t<br/>
interface fastethernet 0/0<br/>
ip address 192.168.7.1 255.255.255.0<br/>
no shut<br/><br/>
exit<br/>
interface serial 2/0<br/>
shut<br/>
ip address 10.10.10.26 255.255.255.252<br/>
no shut<br/><br/>
exit<br/>
router ospf 1<br/>
network 192.168.7.0 0.0.0.255 area 1<br/>
network 10.10.10.24 0.0.0.3 area 1<br/>
exit<br/>
exit<br/>

show ip route ospf<br/><br/>
