# script_tunneling


Setting ROUTER 1
Router>en
Router#config t
Router(config)#int g0/0
Router(config-if)#ip add 11.11.11.2 255.255.255.0
Router(config-if)#no sh
Router(config-if)#int g0/1
Router(config-if)#ip add 12.12.12.1 255.255.255.0
Router(config-if)#no shut


Setting ROUTER 2

Router>en
Router#config t
Router(config)#int g0/0
Router(config-if)#ip add 10.10.10.10 255.255.255.0
Router(config-if)#no shut
Router(config-if)#int g0/1
Router(config-if)#ip add 11.11.11.1 255.255.255.0
Router(config-if)#no sh
Router(config-if)#int tunn0
Router(config-if)#ip add 172.168.1.1 255.255.255.0
Router(config-if)#tunn source g0/1
Router(config-if)#tunn destination 12.12.12.2
Router(config-if)#tunn mode gre ip
Router(config-if)#ex
Router(config)#ip route 13.13.13.0 255.255.255.0 172.168.1.2
Router(config)#ip route 0.0.0.0 0.0.0.0 gig0/1

Setting ROUTER 3

Router>en
Router#config t
Router(config)#int g0/0
Router(config-if)#ip add 13.13.13.10 255.255.255.0
Router(config-if)#no shut
Router(config-if)#int g0/1
Router(config-if)#ip add 12.12.12.2 255.255.255.0
Router(config-if)#no sh
Router(config-if)#int tunn0
Router(config-if)#ip add 172.168.1.2 255.255.255.0
Router(config-if)#tunn source g0/1
Router(config-if)#tunn destination 11.11.11.1
Router(config-if)#ex
Router(config)#ip route 10.10.10.0 255.255.255.0 172.168.1.1
Router(config)#ip route 0.0.0.0 0.0.0.0 gigabitethernet 0/1


IP PC1 : 10.10.10.1 | gw : 10.10.10.10
IP PC2 : 13.13.13.1 | gw : 13.13.13.10
