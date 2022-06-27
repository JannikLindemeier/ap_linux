# Globbing und Quotes
## Quotes
**'' (Singlequotes):** Alles wird maskiert - der Text wird genauso ausgegeben/gespeichert/..., wie er als Text dasteht. 

**"""" (Doublequotes):** Variablen (beginnen mit $) werden durch Inhalt ersetzt, außer sie werden mit einem Backslash maskiert. Auch Befehle in Backticks werden interpretiert. Alles andere (Globs, etc) wird maskiert. 

**\`\` (Backticks):** In Backticks stehender Text wird als Befehl interpretiert und ausgeführt. Globbing-Symbole können auch verwendet werden. 


## Globbing
Mit den Globbing-Symbolen können Masken definiert werden, durch welche die Verzeichnisinhalte gefiltert werden. 

### `*` 
Repräsentiert jedes beliebige Zeichen in jeder Anzahl (auch 0 Zeichen).

### `?`
Ganz genau ein Zeichen (beliebig)

### `[a]`
Genau ein Buchstabe (a)

### `[abc]`
Genau ein Buchstabe aus der Auswahl (a, b oder c)

### `[a-e]`
Genau ein Zeichen aus dem Bereich (a, b, c, d oder e). Die Reihenfolge richtet sich nach der ASCII-Tabelle. 

### `[!a]`
Verneinung des Ausdruckes (Hier: nicht "a", bzw. alles außer "a"). Funktioniert auch mit Aufzählungen (`[!abc]`: Nicht a, b oder c) oder mit Bereichen (`[a-e]`: Kein Zeichen aus dem Bereich a bis e). 

### `{}`
Alle Kombinationen aus den Zeichen. Beispiel: 
```sh
echo {a,b}{1,2}
```
Ausgabe: `a1 a2 b1 b2`

