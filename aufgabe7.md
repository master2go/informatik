# Aufgabe  1
## Wieviele verschiedene Dateitypen gibt es in dem Ordner?
Dazu wird folgender Befehl vorgeschlagen: 

```bash
find . -type f | sed "s/.*\/.*\.//g" | sort | uniq -c | sort -r
```
**Erklärung**
Es sind unterschiedliche Befehle, die jeweils durch eine pipe übergeben werden
1. *find . -type f*
   Der find Befehl kann alle Ordner nach allen möglichen Kriterien dursuchen. Der Punkt hinter find gibt an das ab dem aktuellen Ort bis in alle unterordner gesucht
   werden soll. -type gibt an welche Arten von Dateien gesucht werden sollen. f steht für alle regulären Dateien, also zB keine symbolischen links. | Der gerade Strich ist eine
   Pipe, dh. das Ergebnis des find Befehls wird an sed weitergegeben
2. *sed "s/.*\/.*\.//g"*
   sed ist ein stream editor, eine Art Texteditor. sed kann Texte durchsuchen, das gefunde löschen, ersetzen, austauschen usw. Im vorliegenden Fall, wird dem Befehl sed folgendes mitgegeben: *was* s = ersetzen. *welche Zeichen* /.*\/.*\. dieser Teil besagt welche Zeichen ersetzt werden sollen: alles vor und alles nach dem letzten / einschließlich des Punktes. *Durch was erstetzt: // durch nichts. und das g steht für global Also wende es an so oft es vorkommt
3. sort sortiert das Ergebnis von sed (es bleiben nur noch Dateiendungen übrig) nach dem Alphabet
4. uniq -c zählt wieviele es von jeder Endung gibt
5. sort -r sortiert nach Anzahl
# Aufgabe 2
## wieviele unterschiedliche png sind in dem Ordner und wieviele Versionen gibt es von jeder Datei
Dies lässt sich mit folgendem Befehl lösen:
```bash
find  -type f -name "*.png" -exec sha256sum {} + | sort | uniq -w 64 -c | sort -nr
```
1. Mit *find  -type f -name "*.png"* werden alle Dateien gesucht, die mit .png enden.
2. mit *-exec sha256sum {} +* wird für jede dieser Dateien ein indivdueller hash vergeben (das + sorgt dafür, dass dies im batch Verfahren geschieht.) Dateien die ganz genau gleich sind haben auch den gleichen hash. So können also Dateien auch wenn sie unterschiedliche Namen haben als gleich erkannt werden.
3. Nun wird das Ergebnis sortiert nach dem Alphabet, dann nach Zahlen. Dies ist wichtig, da uniq nur gleiche hashs zählen kann, wenn sie untereinander stehen
4. Mit uniq -c wird das Ergebnis gezählt. Also wieoft kommt ein bestimmter haashtag vor, so viele Versionen gibt es auch von der Datei. -w 64 stellt sicher, dass alle 64 Zeichen des hashs miteinander verglichen werden
5. DUrch das nochmalige sortieren mit -nr wird in absteigender Reihenfolge sortiert und es wird noch ein Dateiname ausgegeben

   
