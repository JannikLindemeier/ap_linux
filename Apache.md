# Apache

## Grundlagen
- Nutzung nach GNU Public License
- Am effizientesten unter UNIX, aber auch Windows-Distributionen verfügbar
- Konfiguration in apache2.conf (hier können aber auch externe Dateien included werden)

### Konfiguration (Auszug)
`Servertype`
- Standalone: Server läuft konstant, Zugriff jederzeit möglich
- Inetd: Server wird nur auf Anfrage gestartet (deprecated)

`ServerRoot`
Pfad für Config-, Error-, und Logfiles

`Listen`
Port(s), unter welchen der Serverprozess lauscht

`ServerAdmin`
E-Mail des Admins (für Fehlermeldungen, ...)

#### Gültigkeitsbereiche
Konfigurationen werden nur auf bestimmte Bereiche Angewendet (HTML/XML-ähnliche Syntax): 
`<VirtualHost>...</VirtualHost>`: Für den gesamten Virtual Host
`<Direcory "PATH">...</Directory>`: Für einen Bereich im Dateisystem des Servers
	`<Files ~ PATTERN>...</Files>`: Für einzelne Dateien in einem Directory
`<Location "URI">...</Location>`: Je nach URI in der Adresszeile

### CLI-Tooling
```sh
a2[en|dis][site|mod|conf] [Objekt]

# Beispiel
a2ensite mysite
```

### Content-Editoren
User anlegen (für andere Nicht-Admins, die nur Inhalte der Website(s) verwalten sollen) + Rechte vergeben auf:
- DocumentRoot (Inhalte der Site)
- Falls vorhanden: .htpasswd für Userverwaltung

Primäre Gruppe: www-data

## Virtual Hosts
Ein Webserver kann mehrere Webseiten (Sites) bereitstellen. Jede Site hat ein eigenes Document Root, wo der Inhalt gespeichert ist. Es gibt drei Arten von Virtual Hosts: 
- Name-Based: Anhand des Hostnames wird entschieden, welche Inhalt angezeigt wird
- IP-Based: Für Server mit mehreren NICs - hier wird anhand der Ziel-IP von der Request unterschieden
- Port-Based: Jede Site läuft über einen anderen Port (ggf. apache2.conf `Ports` und Firewall einstellen)

## Basic Auth
1. **\[SITE\].conf:** `AllowOverride AuthConfig` (in einem Direcory-Block)
2. **.htaccess-Datei im DocumentRoot (oder direkt im Directory-Statement):**
```sh
# /var/www/mysite/html/.htaccess
AuthType Basic
AuthName "MyRealm"
AuthUserFile /var/www/mysite/.htpasswd
AuthGroupFile /var/www/mysite/.htgroups # je nach Anforderung
require valid-user # Oder require user [USER] bzw. require group [GROUP]
```
3. **.htpasswd-Datei:** Nicht im DocumentRoot, soll aber trotzdem vom Content Editor bearbeitbar sein. 
	Hashes generieren: `htpasswd`-Befehl

### Gruppen
Apache-Modul muss aktiviert werden: `a2enmod authz_groupfile`

Gruppenmitgliedschaften stehen in einer `.htgroups`-Datei, Syntax: 
```htgroups
GroupName: user1 user2 user3
```

## HTTPS
**Modul aktivieren:** `a2enmod ssl`
**Pfad für Zertifikate z.B. unter:** /etc/apache2/ssl/SITENAME/{key,cert}.pem

**Selbstsigniertes Zertifikat:**
```sh
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout key.pem -out cert.pem
```

**VirtualHost (separater Host für SSL) konfigurieren:**
```conf
SSLEngine on
SSLCertificateFile PATH
SSLCertificateKeyFile PATH

# Automatisch weiterleiten
Redirect / https://SITE/
```

## LAMP
**LAMP =** Linux Apache MySQL/MariaDB PHP

## CGI (Common Gateway Interface)
Ermöglicht die Bereitstellung von dynamischem Inhalt durch Ausführen von Skripten beim Server (z.B. Bash-Script wird bei Aufruf ausgeführt und gibt HTML aus, welches dann an den Client übermittelt wird).

**Wichtig**
- Script wird mit Berechtigungen des Apache-Daemons ausgeführt (meist in der Gruppe www-data)
	=> ggf. setuid/setgid-Bit setzten
- X-Permission muss gesetzt sein

**Modul aktivieren**
```sh
a2enmod cgi
```

**ScriptAlias in der VirtualHost-Config**
Gibt an, wo die Skripte liegen
```conf
ScriptAlias "/cgi-bin/" "/usr/local/apache2/cgi-bin/"
```

**Scripte erlauben (für Directory)**
```conf
<Directory /var/www/>
	Options ExecCGI
	AddHandler cgi-script .sh # Bestimmte Scripttypen erlauben
</Directory>
```

**Script erstellen (Beispiel):**
```sh
#!/bin/sh
echo "Content-type: text/html"
echo # leere Zeile zwischen Header und Payload
echo "<h1>Hi!</h1>"
```
