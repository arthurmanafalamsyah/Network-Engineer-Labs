This is configuration router on stick


SWITCH
#Vlan 10
#name IT
exit
#Vlan 15
#Name HR
exit

Create VLAN in Switch
#Configure terminal
#interface range ethernet 1/0 - 3
#switchport mode acces
#switchhport acces vlan 10
exit
#Configure terminal
#interface range ethernet 2/0 - 2
#switchport mode acces
#switchport acces vlan 15
exit

Switch to Router
#Configure terminal
#interface ethernet 0/0
#encapsulation dot1q
#switchport mode trunk

Router to Internet
#configure terminal
#interface fastethernet 2/0
#ip address dhcp
or static #ip route 0.0.0.0 0.0.0.0 192.168.1.1 (gateway internet)

Router to vlan, Router->Switch->Vlan 10 and 15
#Configure terminal
#interface fastethernet 0/0.10
#encapsulation dot1q 10
#ip address 192.1.2.1 255.0.0.0
#no shutdown
exit
#interface fastethernet 0/0.15
#encapsulation dot1q 15
#ip address 195.1.3.1 255.128.0.0
#no shutdown

Router create access list to Vlan 10 and 15
#configure terminal
#access-list 1 permit 193.1.2.0 0.255.255.255 (Vlan 10) 1 nama: vlan 10
#access-list 2 permit 195.1.3.0 0.127.255.255 (vlan 15)

Create NAT in Router
#ip nat inside source list 1 interface fastethernet 0/0 overload (Vlan 10)
#ip nat inside source list 2 interface fastethernet 0/0 overload (Vlan 15)

NAT inside and outside in Router
#configure terminal
#interface fastethernet 0/0.10
#ip nat inside
exit
#interface fastethernet 0/0.15
#ip nat inside
exit
#interface fastethernet 2/0 (to internet)
#ip nat outside

SETTING IP PC
Vlan 10 = 193.1.2.2 255.0.0.0 193.1.2.1
Vlan 15 = 195.1.3.2 255.128.0.0 195.1.3.1
