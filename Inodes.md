# Inodes
Linux: Alles ist eine Datei (auch Verzeichnisse, Prozesse, ...). 

**Verzeichnis:** Inode, welche den Verzeichnisinhalt enthält (also Namen verknüpft mit Inode-Nummern) + Selbstverweis und Verweis zum Parent Directory.

**Wurzelverzeichnis:** Inode 2

**Inode:** Entält Verwaltungsinfos (Metadaten), aber nicht den Namen
-   cTime: Erstellungszeitpunkt
-   aTime: Letzter Zugriff
-   mTime: Letzte Änderung
- links_count: Hardlink-Zähler
-   …

