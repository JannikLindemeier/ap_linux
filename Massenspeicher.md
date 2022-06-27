# Harddisks
Alle Geräte werden bei Linux im Dateisystem repräsentiert (`/dev`). Die Namen für SATA-Platten beginnen dabei mit dem Präfix "sd" (=> Pfad: `/dev/sd*`). Disks werden mit Kleinbuchstaben durchnummeriert, Partitionen mit Nummern (beginnend bei 1). 

## Partition erstellen
Festplatte 2 => /dev/sdb

```sh
bash> fdisk /dev/sdb
# Interaktive CLI wird gestartet
	> n # new partition
	Partition type (p: primary; e: extended)
	> p
	Partition number (1-4)
	> 1
	First sector
	> # leer lassen und default verwenden
	Last sector
	> # leer lassen und default verwenden
	> w # write: Änderungen anwenden
```


## High-Level Formatierung
`mkfs -t [DATEISYSTEM] [PFAD ZU PARTITION]`: make filesystem

```sh
bash> mkfs -t ext4 /dev/sdb1 # 2. Platte, 1. Partition
```


## Platte mounten
1. Mountpfad anlegen (z.B. Unterverzeichnis von /media oder /mnt)
2. Platte mounten: `mount [PFAD ZU PARTITION] [ZIEL (Mountpfad)]`
3. Platte auswerfen: `umount [ZIEL (Mountpfad)]`

**Hinweis:** Inhalte im Mountpfadverzeichnis werden "versteckt", wenn auf dieses Verzeichnis ein Datenträger gemountet wird. Nach den unmounten kann man auf die Inhalte wieder zugreifen. 

#HDDs #Massenspeicher