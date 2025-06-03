# Cisco Packet Tracer Parancsok

## Alap parancsok (10. osztály)

### Belépés privilegizált EXEC módba és config módba
```
Router> enable
Router# configure terminal
```

### Eszköznév beállítása
```
Router(config)# hostname [eszköznév]
```

### Privilegizált mód titkosított jelszó beállítása
```
Router(config)# enable secret [jelszó]
```

### Enable mód jelszó beállítása
```
Router(config)# enable password [jelszó]
```

### Konzol jelszó és időtúllépés beállítása
```
Router(config)# line console 0
Router(config-line)# password [jelszó]
Router(config-line)# login
Router(config-line)# exec-timeout [min] [sec]
```

### Felhasználó és jelszó beállítása
```
Router(config)# username [felhasználónév] password [jelszó]
Router(config)# username [felhasználónév] privilege 15 secret [jelszó]
Router(config)# line vty 0 15
Router(config-line)# login local
```

### Jelszó titkosítás beállítása
```
Router(config)# service password-encryption
```

### Minimum jelszó hossz beállítása
```
Router(config)# security passwords min-length [hossz]
```

### Névfeloldás letiltása
```
Router(config)# no ip domain-lookup
```

### Napi banner üzenet beállítása
```
Router(config)# banner motd "Ez egy üzenet"
```

### IPv4 cím beállítása
```
Router(config)# interface [interfész]
Router(config-if)# ip address [IP-cím] [alhálózati maszk]
Router(config-if)# no shutdown
```

### Switchnél IPv4 cím beállítása és alapértelmezett átjáró beállítása
```
Switch(config)# interface vlan 1
Switch(config-if)# ip address [IP-cím] [alhálózati maszk]
Switch(config-if)# no shutdown
Switch(config-if)# exit
Switch(config)# ip default-gateway [IP-cím]
```

### IPv6 bekapcsolása
```
Router(config)# ipv6 enable
Router(config)# ipv6 unicast-routing
```

### IPv6 cím és link-local cím beállítása
```
Router(config)# interface [interfész]
Router(config-if)# ipv6 address [IPv6-cím]/[hossz]
Router(config-if)# ipv6 address autoconfig
Router(config-if)# ipv6 address dhcp
Router(config-if)# ipv6 address [link-local cím] link-local
Router(config-if)# no shutdown
```

### Tartománynév beállítása
```
Router(config)# ip domain-name [tartománynév]
```

### Titkosítás beállítása (RSA kulcs generálása)
```
Router(config)# crypto key generate rsa
(modulus)# [kulcshossz]
```

### SSH verzió, időtúllépés és újrapróbálkozási lehetőség beállítása
```
Router(config)# ip ssh version 2
Router(config)# ip ssh time-out [másodperc]
Router(config)# ip ssh authentication-retries [szám]
```

### Telnet beállítása és bekapcsolása
```
Router(config)# line vty 0 15
Router(config-line)# transport input telnet
Router(config-line)# login local
```

### Futó konfiguráció megtekintése és mentése az NVRAM-ba
```
Router# show running-config
Router# copy running-config startup-config
```

_______________________________________________
_______________________________________________
_______________________________________________

## További parancsok (11. osztály)

### Switch: VLAN létrehozása és név hozzáadása
```
Switch(config)# interface vlan [szám]
Switch(config-if)# exit
Switch(config)# vlan [szám]
Switch(config-vlan)# name [név]
```

### Switch: Interfész hozzárendelése egy VLAN-hoz (hozzáférési portként beállítás)
```
Switch(config)# interface [interfész]
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan [szám]
```

### Switch: Több interfész hozzárendelése egy VLAN-hoz (hozzáférési portként beállítás)
```
Switch(config)# interface range [interfész]/[1. interfész szám]-[utolsó interfész szám]
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan [szám]
```

### Switch: VLAN konfiguráció/hozzárendelés megtekintése
```
Switch# show vlan
Switch# show vlan brief
```

### Switch: Interfésznél trönk mód beállítása
```
Switch(config)# interface [interfész]
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport nonegotiate
Switch(config-if)# switchport trunk allowed vlan [szám],[szám]
```

#### Natív VLAN beállítása
```
Switch(config-if)# switchport trunk native vlan [szám]
```

### Switch: Trönk konfiguráció/hozzárendelés megtekintése
```
Switch# show interface trunk
```

----------------------------------

### Router-on-a-Stick Inter-VLAN Routing beállítása

#### Alinterfész létrehozása
```
Router(config)# interface [interfész].[alinterfész szám]
```

#### 802.1Q (Dot1Q) encapsulation beállítása
```
Router(config-subif)# encapsulation dot1Q [VLAN szám]
Router(config-subif)# ip address [IP-cím] [Alhálózati Maszk]
```

#### Aliterfészek megtekintése
```
Router# show ip interface brief
```

----------------------------------

### Switch: Spanning-tree protokoll

#### Root bridge beállítása

```
Switch(config)# spanning-tree vlan [szám] root primary
```

#### Root bridge beállítása: BID Prioritási érték beállítása (alacsonyabb számú a root bridge)

```
Switch(config)# spanning-tree vlan [szám] priority [szám]
```

#### Ellenőrzés

```
Switch# show spanning-tree
```

----------------------------------

### Switch: EtherChannel

#### Kábelek kiválasztása

```
Switch(config)# interface range [interfész]/[1. interfész szám]-[utolsó interfész szám]
```

#### PAgP beállítása (**desirable**, vagy auto)

```
Switch(config-if-range)# channel-group [csoportszám] mode [mód neve, preferált: desirable]
```

#### LACP beállítása (**active**, vagy passive)

```
Switch(config-if-range)# channel-group [csoportszám] mode [mód neve, preferált: active]
```

#### Csoport konfigurálása

```
Switch(config)# interface port-channel [szám]
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan [szám],[szám]
```

#### Ellenőrzés

```
Switch# show interfaces port-channel [szám]
Switch# show etherchannel summary
Switch# show etherchannel port-channel
Switch# show interfaces [interfész] etherchannel
```

----------------------------------

### Router: DHCPv4 beállítása

#### DHCP Pool létrehozása

```
Router(config)# ip dhcp pool [név]
```

#### Hálózati cím beállítása

```
Router(dhcp-config)# network [cím] [alhálózati maszk]
```

#### Alapértelmezett átjáró

```
Router(dhcp-config)# default-router [cím]
```

#### DNS szerver

```
Router(dhcp-config)# dns-server [cím]
```

#### Domain név

```
Router(dhcp-config)# domain-name [cím]
```

#### IP címek kizárása

```
Router(config)# ip dhcp excluded-address [kezdő cím] [végső cím]
```

#### Ellenőrzés

```
Router# show running-config | section dhcp
Router# show ip dhcp binding
Router# show ip dhcp pool
```

----------------------------------

### Router: Virtuális HSRP (Hot Standby Router Protocol) Router beállítása

#### HSRP verzió beállítása

```
Router(config)# interface [interfész]
Router(config-if)# standby version 2
```

#### Virtuális IP cím beállítása

```
Router(config-if)# standby [csoportszám] ip [IP cím]
```

#### Prioritás beállítása (magassab számú az aktív)

```
Router(config-if)# standby [csoportszám] priority [szám]
```

#### Preemption (Prioritásos szerepátvétel) engedélyezése

```
Router(config-if)# standby [csoportszám] preempt
```

----------------------------------

### Router: RIP (Routing Information Protocol) aktiválása és hálózati címek konfigurálása

```
Router(config)# router rip
Router(config-router)# network [hálózati cím]
```

----------------------------------

### Router: helper address beállítása (DHCP-hez)

```
Router(config)# interface [interfész]
Router(config-if)# ip helper-address [IP cím]
```

----------------------------------

### Router: Stateful DHCPv6 beállítása

#### DHCP Pool létrehozása

```
Router(config)# ipv6 dhcp pool [név]
```

#### Hálózati cím beállítása

```
Router(config-dhcpv6)# prefix-delegation pool [DHCP pool neve]
Router(config-dhcpv6)# address prefix [cím]/[hossz/prefix]
```

#### DNS szerver

```
Router(config-dhcpv6)# dns-server [cím]
```

#### Domain név

```
Router(config-dhcpv6)# domain-name [cím]
```

#### Adott interfészhez a dhcp pool hozzárendelése

```
Router(config)# interface [interfész]
Router(config-if)# ipv6 dhcp server [dhcp-pool neve]
Router(config-if)# ipv6 nd managed-config-flag
```

#### Ellenőrzés

```
Router# show ipv6 dhcp binding
Router# show ipv6 dhcp interface
Router# show ipv6 dhcp pool
```

----------------------------------

### Router: Stateless DHCPv6 beállítása

#### DHCP Pool létrehozása

```
Router(config)# ipv6 dhcp pool [név]
```

#### DNS szerver

```
Router(config-dhcpv6)# dns-server [cím]
```

#### Domain név

```
Router(config-dhcpv6)# domain-name [cím]
```

#### Adott interfészhez a dhcp pool hozzárendelése

```
Router(config)# interface [interfész]
Router(config-if)# ipv6 dhcp server [dhcp-pool neve]
Router(config-if)# ipv6 nd other-config-flag
```

#### Ellenőrzés

```
Router# show ipv6 dhcp binding
Router# show ipv6 dhcp interface
Router# show ipv6 dhcp pool
```

----------------------------------
