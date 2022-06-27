# Dateirechte

## chmod
Ändern von Berechtigungen

### Einfache Variante
```sh
chmod [PARTEI][+|-][PERMISSION] [PFAD]
# z.B. chmod g+r /test.txt => Leseberechtigung für die Gruppe auf test.txt
# a+ für alle Parteien
# Partei: u, g oder o
```

### Binäre Permissions
```sh
chmod UGO [PFAD]
# z.B. chmod 700 /test.sh
# Vollzugriff für User, Gruppe und Others dürfen nichts
```

**Stellenwerte:**
Read | Write | Execute/Verzeichnis betreten
-- | -- | --
2<sup>2</sup> | 2<sup>1</sup> | 2<sup>0</sup>

## umask
Bearbeitet die Berechtigungen, welche beim Erstellen eines Objektes standardmäßig vergeben werden. 
```sh
umask MASK
```

Die Maske wird von festen Werten subtrahiert:
- Datei: 666
- Verzeichnis: 777

**Beispiel:**
`umask 007`

Dateirechte: 660
Orderrechte: 770

## Spezialbits
```sh
chmod [SPEZIALBIT] [PERMISSIONS] [PFAD]
```

**Stellenwerte:**
setuid | setgid | sticky
-- | -- | --
4 | 2 | 1

### setuid
Berechtigung: `rws-***-***`
Befehl wird mit den Dateiowner-Berechtigungen ausgeführt. 

### setgid
Berechtigung: `***-rws-***`
**Datei:** Befehl wird mit Rechten der Owner-Gruppe ausgeführt
**Verzeichnis:** Neue Dateien haben die Owner-Gruppe des Elternverzeichnisses statt die der User-Primary-Group. 

## sticky-bit
Berechtigung: `***-***-rwt`
Nur der Owner darf das Objekt löschen

## Links
### Hardlinks
Weiterer Eintrag, der auf die Inode des Ziels verweist. 
- Link und Ziel sind auf selber Platte, da jeder Datenträger eine eigene Inode-Verwaltung hat. 
- Erhöht Hardlink-Counter

### Symlinks
Weiterer Eintrag mit eigener Inode. Dateiinhalt ist der Zielpfad
- Kopieren: Ziel wird kopiert
- Verschieben/umbennen/löschen: Betrifft den Link selbst