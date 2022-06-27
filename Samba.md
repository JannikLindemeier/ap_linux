# Samba
Windows-Server-Dienste werden Linux-basiert bereitgestellt. 

- "Windows-Server" auf Linux-System aufsetzen
- Alle Clients ab Windows-DOS + Linux-Systeme

**Voraussetzung:** TCP/IP mit NBT (NetBIOS over TCP/IP)
**Aktuelle Version:** 4.x

**Pakete:**
- `samba`
- `smbclient`
- `samba-doc`


## Begriffe
**NetBIOS:** Network basic input output system. Ist KEIN Protokoll, sondern ein Kommunikationsstandard, welcher auf ein anderes Protokoll aufsetzt.
**NBT:** NetBIOS over TCP/IP (Früher: NetBEUI, propietär und nicht routingfähig)
**SMB:** Server Message Block-Protokoll (Datei- und Druckerfreigabe unter Windows; entwickelt von IBM)
**CIFS:** Common Internet File System (SMB-Implementierung von Microsoft; CIFS ist ein "SMB-Dialekt"; die Protokolle sind miteinander kompatibel)
**RID:** Relative Identifier. Eindeutiger Identifier für einen User (nur den User) innerhalb der Domäne.
**SID:** Security Identifier. Die SID für einen User setzt sich zusammen aus der SID der Domäne und dem RID des Users. 

**Arbeitsgruppe:** 
- Liste von Rechnern
- Unterverzeichnis in einer Windows-Netzwerk-Umgebung

**Domäne:**
- Zentrale Verwaltung von User- und Computeraccounts
- Verzeichnis in einer Windows-Netzwerk-Umgebung


## Typen von Samba-Servern
- Stand-alone (Workgroup)
- Integriert in eine Domäne
- Domain Controller
- Active Directory Server (ab Version 4)

## Prozesse
### smbd
- stellt Verzeichnisse im Netzwerk bereit
- Drucker/Druckdienste
- Authentifizierung und Berechtigungen

### nmbd
- Auflösung von NetBIOS-Namen
- WINS (veralteter Namensauflöser für NetBIOS-Namen)
- Bereitstellung von Browsing-Listen für Windows Network Neighborhood (Infos über andere Rechner im Netz)
- Teilnahme an Local Master-Wahlen

### winbind
Authentifizierungsdient bei Domänen
- User/Computer
- Zuordnung von SID/RID mit Unix-UID und GID

## WINS
**Local Master Browser (LMB):** Verwaltet Liste von Rechnern (Suchliste/Browse List) in einer Arbeitsgruppe/Domain. Andere Rechner fragen hier nach einer Liste ihrer "Nachbarn".

### Local Master-Konfiguration
Der Local Master wird gewählt. Verschiedene Parameter bestimmen, wer die Wahl gewinnt: 

`local master`: Legt fest, ob der Server an Wahlen teilnimmt
`preferred master`: Erzwingt beim Start des nmbd-Dienstes eine (Neu)Wahl. 
`os level`: Eine Art "Priorität" bei der Wahl. Werte zwischen 0 und 255. Der Rechner mit dem höchsten Wert gewinnt die Wahl. 


## Befehle
### Config überprüfen
```sh
testparm [PFAD CONFIG-DATEI]
```



