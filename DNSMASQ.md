# dnsmasq
Einfacher [[DNS]]- und DHCP-Server für SOHO-Umgebungen. Alternativ: 
- DNS: [[Bind & Webmin]]
- DHCP: [[ISC DHCP-Server]]

**Paketname:** `dnsmasq`

**Konfiguration testen**
```sh
dnsmasq --test -C /etc/dnsmasq.conf
```

## DNS
- Namen aus `/etc/hosts` werden aufgelöst
- Unbekannte Namen: Anfragen werden weitergeleitet und gecached

## DHCP
**Wichtig:** NIC muss statisch konfiguriert sein (+ NIC neustarten)

Konfiguration in `/etc/dnsmasq.conf`
- interface (oder no-dhcp-interface)
- dhcp-range
- Optionen (z.B. option:dns-server)


#DNS #DHCP