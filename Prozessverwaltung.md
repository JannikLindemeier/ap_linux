# Prozessverwaltung
## Shortcuts
`[CTRL] + C`: Prozess beenden
`[CTRL] + Z`: Prozess anhalten (pausieren)

## Signale zur Prozesssteuerung
Code | Bedeutung
-- | --
SIGKILL | Sofort beenden (killen), ohne zu speichern, ...
SIGTERM | Prozess auffordern, freiwillig zu beenden
SIGSTOP | Prozess anhalten (CPU-Zeit wird entzogen)
SIGCONT | Angehaltenen Prozess fortsetzen

## Prozesshierarchie
Unter Linux sind Prozesse hierarchisch angeordnet - ein Elternprozess kann Kindprozesse starten. 

**PID:** Process ID
**PPID:** Parent Process ID

Der Prozess mit der ID 1 ist der Initprozess (wird als erstes gestartet und ist Vater aller anderen Prozesse). Wird er gekillt, fährt das System herunter (d.h. Root-Rechte zum beenden notwendig). 

## Daemons
Systemrelevant Prozesse (z.B. Netzwerkanbindung, Druckausgabe, ...), welche im Hintergrund laufen und nicht interaktiv vom User gestartet werden. 

## Zombies
**Vorab:** Jeder Prozess gibt beim Beenden einen Exit-Status zurück. Dieser muss vom Elternprozess entgegengenommen werden. 

**Entstehung:** Zombie-Prozesse entstehen, wenn der Kindprozess beendet wird, der Elternprozess den Exit-Status jedoch nicht entgegennimmt. 
Der Kindprozess läuft zwar nicht mehr (und erhält auch keine Betriebsmittel), kann jedoch nicht aus der Prozesstabelle entfernt werden, solang der der Elternprozess den Status nicht entgegennimmt.

**Beispiel-Script, um Zombies zu erzeugen:**
![[Pasted image 20220615004952.png]]


## Zustände und Übergänge
### Zustände
**running:** Prozess wird gerade ausgeführt
**runnable (R):** Prozess läuft nicht, kann aber ausgeführt werden
**sleeping (S):** Prozess schläft und wartet auf Rechenzeit
**uniterruptible sleep (D):** Prozess ist im kernel space (Systemaufruf). Prozess kann nicht abgebrochen werden
**stopped (T):** Angehalten, kann später weiterlaufen
**zombie (Z):** Zombieprozess

### Übergänge
![[Pasted image 20220615171808.png]]

## Befehle
**Prozess:** Ein einzelnes Programm, welches gerade ausgeführt wird. 

**Job:** Konzept der Shell. Ein interaktiv gestartetes Programm (z.B. kein Daemon) - kann eine Gruppierung aus mehreren Prozessen sein. 

### Jobs
Laufende Jobs anzeigen
```sh
jobs

# Optionen
-l PID ausgeben
```
<sub>
<b>Plus/Minus-Symbole in der Ausgabe: </b>
<br>
<b>+:</b> Dieser Job ist der Default, falls fg/bg ohne Argumente aufgerufen werden.
<br>
<b>-:</b> Wird der neue Default, falls der aktuelle "+"-Prozess beendet wird. 
</sub>

Job/Prozess beenden
```sh
kill -s [SIGNAL] [PID] # Prozess beenden (PID)
kill %[JOB_SPEC] # Job beenden (Job-Nummer mit %)
```

Pausierten Job fortsetzen
```sh
fg %[JOB_SPEC] # Im Vordergrund
bg %[JOB_SPEC] # Im Hintergrund
```

### Prozesse
Permanent aktualisiert
```sh
top
```

Einmaliger Snapshot
```sh
ps

# Optionen 
-e # Alle Prozesse anzeigen (auch andere User)
-l # Langes Format bei der Ausgabe (erweiterte Infos)
-f # Formatieren (z.B. statt UID wird Username angezeigt)
```

#Prozesse #Prozesse/Linux