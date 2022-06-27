# DNS
**Dienst anbieten mit:**
- [[Bind & Webmin]]
- [[DNSMASQ]]

## Auflösung unter Linux
1. Lookup in der `/etc/hosts`
2. Nameserver aus `/etc/resolv.conf`
	- Lokaler Nameserver kann auflösen
		- Bei Eintrag im Cache
		- Wenn er die Zone verwaltet
	- Anderenfalls: normale Namensauflösung (Weiterleitung)

**/etc/resolv.conf:**
- Enthält die DNS-Konfiguration des Rechners
- Bei DHCP: wird automatisch konfiguriert

## Record-Typen
Typ | Beschreibung
-- | --
A | IPv4
AAAA | IPv6
A6 | IPv6
CNAME | Alias
NS | Nameserver Record
MX | Mailserver
SOA | Start of Authority (Verwaltungsinfos)
PTR | Pointer für Reverse-DNS
HINFO | Host-Info (Text) (selten)
TXT | Freier Text
RP | Responsible Person (selten)

**Experimentell/ungebräuchlich**
Typ | Beschreibung
-- | --
ISDN | Telefonnummer
MINFO | Mailbox/Mailinglisten-Info
NULL | Tut nichts


#DNS

