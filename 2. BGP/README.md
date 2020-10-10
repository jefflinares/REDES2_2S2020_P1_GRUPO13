## BGP

- AS 100
Router 0 (OPSF)
Router(config)#interface serial 8/0
Router(config-if)#ip address 10.1.4.0 255.255.255.252
Bad mask /30 for address 10.1.4.0
Router(config-if)#ip address 10.1.4.1 255.255.255.252
Router(config-if)#no shut


Router 4

```bash
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.


Router(config)#interface serial 3/0
Router(config-if)#ip address 10.1.1.2 255.255.255.252
Router(config-if)#no shut

Router(config-if)#
%LINK-5-CHANGED: Interface Serial3/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Serial3/0, changed state to up

Router(config-if)#exit
Router(config)#interface serial 2/0
Router(config-if)#ip address 10.1.2.1 255.255.255.252
Router(config-if)#no shut

Router(config-if)#
%LINK-5-CHANGED: Interface Serial2/0, changed state to up

Router(config-if)#exit
Router(config)#ip address 10.1.2.1 255.255.255.252


%LINEPROTO-5-UPDOWN: Line protocol on Interf
Router(config)#interface fastEthernet 0/0
Router(config-if)#ip address 192.10.3.1 255.255.255.0
Router(config-if)#no shut

Router(config-if)#
%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0, changed state to up

Router(config-if)#exit



Router(config)#interface serial 6/0
Router(config-if)#ip address 10.1.4.2 255.255.255.252
Router(config-if)#no shut

Router(config-if)#
%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0, changed state to up

Router(config-if)#exit


Router(config)#router bgp 100
Router(config-router)#network 10.1.1.0 mask 255.255.255.252
Router(config-router)#network 10.1.2.0 mask 255.255.255.252
Router(config-router)#network 10.1.4.0 mask 255.255.255.252
Router(config-router)#network 192.10.3.0 mask 255.255.255.0
Router(config-router)#exit


Router(config)#router bgp 100
Router(config-router)#neighbor 10.1.1.1 remote-as 300
Router(config-router)#%BGP-5-ADJCHANGE: neighbor 10.1.1.1 Up
neighbor 10.1.2.2 remote-as 200
Router(config-router)#%BGP-5-ADJCHANGE: neighbor 10.1.2.2 Up

#show ip bgp neighbors


``` 

- AS 200

Router 5

```bash
Router>en
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface serial 2/0
Router(config-if)#ip address 10.1.3.2 255.255.255.252
Router(config-if)#no shut

%LINK-5-CHANGED: Interface Serial2/0, changed state to down
Router(config-if)#exit
Router(config)#interface serial 3/0
Router(config-if)#ip address 10.1.2.2 255.255.255.252
Router(config-if)#no shut


Router(config)#interface fastEthernet 0/0
Router(config-if)#ip address 192.10.1.1 255.255.255.0
Router(config-if)#no shut

Router(config-if)#exit



Router(config)#router bgp 200
Router(config-router)#network 10.1.2.0 mask 255.255.255.252
Router(config-router)#network 10.1.3.0 mask 255.255.255.252
Router(config-router)#network 192.10.1.0 mask 255.255.255.0

#Agregar vecinos
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#router bgp 200
Router(config-router)#neighbor 10.1.2.1 remote-as 100
Router(config-router)#neighbor 10.1.3.1 remote-as 300


```
- AS 300

Router 3
```bash
Router>en
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface serial 2/0
Router(config-if)#ip address 10.1.3.1 255.255.255.252
Router(config-if)#no shut
Router(config-if)#exit


Router(config)#interface serial 3/0
Router(config-if)#ip address 10.1.1.1 255.255.255.252
Router(config-if)#no shut

%LINK-5-CHANGED: Interface Serial3/0, changed state to down
Router(config-if)#exit


Router(config)#interface fastEthernet 0/0
Router(config-if)#ip address 192.10.2.1 255.255.255.0
Router(config-if)#no shut

Router(config-if)#exit


Router(config)#router bgp 300
Router(config-router)#network 10.1.1.0 mask 255.255.255.252
Router(config-router)#network 10.1.3.0 mask 255.255.255.252
Router(config-router)#network 192.10.2.0 mask 255.255.255.0


#agregar vecinos
Router(config-router)#neighbor 10.1.1.2 remote-as 100
Router(config-router)#neighbor 10.1.3.2 remote-as 200
Router(config-router)#%BGP-5-ADJCHANGE: neighbor 10.1.3.2 Up


```

