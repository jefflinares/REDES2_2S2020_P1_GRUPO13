# Red de telefonica

Telefonica le pide que configure una red con una topología de 3 Capas y que en enrutamiento se realice por medio de un protocolo RIP. (6 routers mínimo, 10 Hosts, distribuidos de la manera que usted considere prudente.).

## Red disponible

La redes disponibles para telefonica son las siguientes

| VLAN | Nombre       | Dirección de red   | Primera dirección asignable | Ultima dirección asignable | Dirección de broadcast |
| ---- | ------------ | ------------------ | --------------------------- | -------------------------- | ---------------------- |
| 10   | RHUMANOS     | 192\.168\.45\.0/24 | 192\.168\.45\.1             | 192\.168\.45\.254          | 192\.168\.45\.255      |
| 20   | CONTABILIDAD | 192\.168\.46\.0/24 | 192\.168\.46\.1             | 192\.168\.46\.254          | 192\.168\.46\.255      |
| 30   | VENTAS       | 192\.168\.47\.0/24 | 192\.168\.47\.1             | 192\.168\.47\.254          | 192\.168\.47\.255      |
| 40   | DESARROLLO   | 192\.168\.48\.0/24 | 192\.168\.48\.1             | 192\.168\.48\.254          | 192\.168\.48\.255      |

## Configuración utilizada

### SW1

```
ena
conf t
vlan 10
name RHUMANOS
vlan 20
name CONTABILIDAD
vlan 30
name VENTAS
vlan 40
name DESARROLLO
exit
exit
show vlan

conf t
int fa0/1
switchport mode access
switchport access vlan 10
int fa0/2
switchport mode access
switchport access vlan 20
int fa0/7
switchport mode access
switchport access vlan 30
exit

int fa0/3
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
int fa0/6
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
exit
exit

```

### SW2

```
ena
conf t
vlan 10
name RHUMANOS
vlan 20
name CONTABILIDAD
vlan 30
name VENTAS
vlan 40
name DESARROLLO
exit
exit
show vlan

conf t
int fa0/1
switchport mode access
switchport access vlan 40
int fa0/2
switchport mode access
switchport access vlan 10
int fa0/7
switchport mode access
switchport access vlan 20
exit

int fa0/3
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
int fa0/6
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
exit
exit

```

### SW3

```
ena
conf t
vlan 10
name RHUMANOS
vlan 20
name CONTABILIDAD
vlan 30
name VENTAS
vlan 40
name DESARROLLO
exit
exit
show vlan

conf t
int fa0/1
switchport mode access
switchport access vlan 40
int fa0/2
switchport mode access
switchport access vlan 30
int fa0/7
switchport mode access
switchport access vlan 10
int fa0/8
switchport mode access
switchport access vlan 20
exit

int fa0/3
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
int fa0/6
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
exit
exit

```

### ESW1

```
ena
conf t
vlan 10
name RHUMANOS
vlan 20
name CONTABILIDAD
vlan 30
name VENTAS
vlan 40
name DESARROLLO
exit
exit
show vlan

conf t
int gig1/0/1
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport trunk encapsulation dot1q
switchport mode trunk
int gig1/0/3
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport trunk encapsulation dot1q
switchport mode trunk
int gig1/0/10
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport trunk encapsulation dot1q
switchport mode trunk
int gig1/0/8
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport trunk encapsulation dot1q
switchport mode trunk
exit

ip routing
interface vlan 10
ip address 192.168.45.1 255.255.255.0
no shutdown
exit
interface vlan 20
ip address 192.168.46.1 255.255.255.0
no shutdown
exit
interface vlan 30
ip address 192.168.47.1 255.255.255.0
no shutdown
exit
interface vlan 40
ip address 192.168.48.1 255.255.255.0
no shutdown
exit
exit

show ip route

```

### ESW2

```
ena
conf t
vlan 10
name RHUMANOS
vlan 20
name CONTABILIDAD
vlan 30
name VENTAS
vlan 40
name DESARROLLO
exit
exit
show vlan

conf t
int gig1/0/8
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport trunk encapsulation dot1q
switchport mode trunk
int gig1/0/4
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport trunk encapsulation dot1q
switchport mode trunk
int gig1/0/2
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport trunk encapsulation dot1q
switchport mode trunk
int gig1/0/9
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport trunk encapsulation dot1q
switchport mode trunk
exit

ip routing
interface vlan 10
ip address 192.168.45.1 255.255.255.0
no shutdown
exit
interface vlan 20
ip address 192.168.46.1 255.255.255.0
no shutdown
exit
interface vlan 30
ip address 192.168.47.1 255.255.255.0
no shutdown
exit
interface vlan 40
ip address 192.168.48.1 255.255.255.0
no shutdown
exit
exit

show ip route

```

### PC

```
DHCP

```

### R34

```
ena
conf t
int se0/2/1
ip address 172.16.0.1 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/3/0
ip address 172.18.0.1 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/2/0
ip address 172.17.0.1 255.255.255.0
clock rate 128000
no shut
end


show ip int brief


conf t
router rip
version 2
network 192.168.45.0
network 192.168.46.0
network 192.168.47.0
network 192.168.48.0
network 172.16.0.0
network 172.17.0.0
network 172.18.0.0
no auto-summary
end

```

### R17

```
ena
conf t
int se0/2/1
ip address 172.16.0.2 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/3/0
ip address 172.19.0.1 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/2/0
ip address 172.20.0.1 255.255.255.0
clock rate 128000
no shut
end


show ip int brief

conf t
router rip
version 2
network 172.16.0.0
network 172.19.0.0
network 172.20.0.0
no auto-summary
end


```

### R19

```
ena
conf t
int se0/2/1
ip address 172.23.0.1 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/3/0
ip address 172.22.0.1 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/2/0
ip address 172.20.0.2 255.255.255.0
clock rate 128000
no shut
end


show ip int brief

conf t
router rip
version 2
network 172.20.0.0
network 172.22.0.0
network 172.23.0.0
no auto-summary
end


```

### R18

```
ena
conf t
int se0/2/1
ip address 172.21.0.1 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/3/0
ip address 172.19.0.2 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/2/0
ip address 172.17.0.2 255.255.255.0
clock rate 128000
no shut
end


show ip int brief

conf t
router rip
version 2
network 172.17.0.0
network 172.19.0.0
network 172.21.0.0
no auto-summary
end



```

### R20

```
ena
conf t
int se0/2/1
ip address 172.21.0.2 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/3/0
ip address 172.22.0.2 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/2/0
ip address 172.24.0.1 255.255.255.0
clock rate 128000
no shut
end


show ip int brief


conf t
router rip
version 2
network 172.21.0.0
network 172.22.0.0
network 172.24.0.0
no auto-summary
end


```

### R21

```
ena
conf t
int se0/2/1
ip address 172.24.0.2 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/3/0
ip address 172.18.0.2 255.255.255.0
clock rate 128000
no shut
end

conf t
int se0/2/0
ip address 172.23.0.2 255.255.255.0
clock rate 128000
no shut
end


show ip int brief


conf t
router rip
version 2
network 172.18.0.0
network 172.23.0.0
network 172.24.0.0
no auto-summary
end

show ip route

```




<!-- Esto no se si esta bien -->
<!-- ### R1

```
ena
vlan database
vlan 10 name RHUMANOS
vlan 20 name CONTABILIDAD
vlan 30 name VENTAS
vlan 40 name DESARROLLO
exit
show vlan

-----------------
conf t
int fa0/0
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
int gig0/2
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
int gig0/3
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
exit
exit
------------

conf t
ip routing
interface vlan 10
ip address 192.168.45.1 255.255.255.0
no shutdown
exit
interface vlan 20
ip address 192.168.46.1 255.255.255.0
no shutdown
exit
interface vlan 30
ip address 192.168.47.1 255.255.255.0
no shutdown
exit
interface vlan 40
ip address 192.168.48.1 255.255.255.0
no shutdown
exit
exit

show ip route

conf t
ip dhcp pool vlan10
network 192.168.45.0 255.255.255.0
default-router 192.168.45.1
dns-server 8.8.8.8
dns-server 8.8.4.4
exit
ip dhcp pool vlan20
network 192.168.46.0 255.255.255.0
default-router 192.168.46.1
dns-server 8.8.8.8
dns-server 8.8.4.4
exit
ip dhcp pool vlan30
network 192.168.47.0 255.255.255.0
default-router 192.168.47.1
dns-server 8.8.8.8
dns-server 8.8.4.4
exit
ip dhcp pool vlan40
network 192.168.48.0 255.255.255.0
default-router 192.168.48.1
dns-server 8.8.8.8
dns-server 8.8.4.4
exit
end
show ip dhcp pool vlan10
show ip dhcp pool vlan20
show ip dhcp pool vlan30
show ip dhcp pool vlan40

```

### R2

```
ena
conf t
vlan 10
name RHUMANOS
vlan 20
name CONTABILIDAD
vlan 30
name VENTAS
vlan 40
name DESARROLLO
exit
exit
show vlan

conf t
int fa0
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
int fa1
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
int fa2
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,30,40,99
switchport mode trunk
exit
exit

``` -->