# ISC DHCP-Server

## Installation
**Paketname:** `isc-dhcp-server`


## Konfiguration
### NIC
Netzwerkinterface muss statisch konfiguriert sein, damit der Dienst gestartet werden kann. 

**Nach der Konfiguration:** Interface oder System muss neugestartet werden. 

### Serverkonfiguration
`/etc/default/isc-dhcp-server`

- Interfaces festlegen (statisch konfiguriert; über diese wird DHCP angeboten; v4 und ggf. v6)
- Falls abweichend vom Default: Pfad zu PID und dhcpd.conf


### Dienstkonfiguration (dhcpd.conf)
`/etc/dhcp/dhcpd.conf`

- DHCP-Pools
- Dienst als Authoritativ deklarieren
- Address reservations
- DNS für dynamische Adressen updaten (ddns-update-style ad-hoc)
- ...

**Konfigurationsebenen:**
- Global (für alle)
- Gruppe (z.B. für ein Subnetz)
- Host (z.B. Address reservations)


#DHCP 