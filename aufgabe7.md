# Teil 1
## Wieviele verschiedene Dateitypen gibt es in dem Ordner?
Dazu wird folgender Befehl vorgeschlagen: 

```bash
find . -type f | sed "s/.*\/.*\.//g" | sort | uniq -c | sort -r
```
**Erklärung**
Es sind unterschiedliche Befehle, die jeweils durch eine pipe übergeben werden
1. *find . -type f* Der find Befehl kann alle Ordner nach allen möglichen Kriterien dursuchen. Der Punkt hinter find gibt an das ab dem aktuellen Ort bis in alle unterordner gesucht
   werden soll. -type gibt an welche Arten von Dateien gesucht werden sollen. f steht für alle regulären Dateien, also zB keine symbolischen links. | Der gerade Strich ist eine
   Pipe, dh. das Ergebnis des find Befehls wird an sed weitergegeben
2. *sed "s/.*\/.*\.//g"* 

   
