## 2.1 Grundlagen 

Variablen festlegen
```bash
declare -u NAME
declare -i INTERGER_VARIABLE
declare -r LESBARE_VARIABLE
```

Konstante definieren
```bash
var="wert"
readonly var
```

## 2.2 Zahlen


Integer-Arithmetik auf alte Art (Bourne-Shell)
```bash
expr 8 / 2
```

problematische Befehle durch Sonderzeichen
```bash
expr 8 * 5  #führt du Problemen 
expr ( 5 + 5 ) * 5  #führt du Problemen 
```

kritische Zeichen mit Backslash verwenden
```bash
expr 8 \* 5  #führt du Problemen 
expr \( 5 + 5 \) \* 5  #führt du Problemen 
```

arithems Ergebniss in Variable speicher durch Kommando-Substitution
```bash
var3=$(expr $var1 + $var2)
```

Integer-Arithmetik für z-shell, korn-shell und bash
```bash
((z=5+5))
echo $z
```

alternative Schreibweise
```bash
z=$((8+8))
echo $y
```

alternative Schreibweise (nur Bash!)
```bash
z=$[8+8]
echo $y
```

Kommando let, wertet arithemtische Ausdrücke aus
```bash
varA=100
varB=50
let varC=$varA+%varB
```

Variable als Integer deklaieren mit typeset
```bash
typeset -i c
a=5
b=2
c=a+b
c=\(a+b\)*2 #Backslash für * nicht mehr notwendig, für Klammern weiterhin
```

Verarbeitungsgeschwindigkeit
```bash
(()) #interne Funktion, viel schneller als
expr
```

Rechnen mit bc (s.h. Seite 134)
```bash
varSQRT=$(echo "scale 5 ; sprt($varA)" | bc)
varSQRT=$(echo "scale 5 ; $varA+$varB" | bc)
```

Zahlen konvertieren
Bin2Dez
```bash
dez=$(echo "obase=10 ; ibase=2 ; $var" | bc)
```

## 2.3 Zeichenketten

schneiden mit cut, fünften character aus jeder Zeile extrahieren
```bash
cut -c5  text.txt
```

fünften bis zehnten character aus jeder Zeile extrahieren
```bash
cut -c5-10  text.txt
```

aus einer mit Semikolon getrennten Liste die erste und dritte Spalte extrahieren
```bash
cut -d\; -f1,3 datei.csv
```

einfügen mit paste, zeilenweisen zusammenführen zweier Dateien
```bash
paste namen.txt nummern.txt > zusammen.txt
```

Lösung mit Trennzeichen ;
```bash
paste -d \; namen.txt nummern.txt > zusammen.txt
```

Zeichen ersetzen mit dem Filter tr, Trennzeichen ; wird durch Tabulator ersetzt
```bash
cut -d\; -f1,3 datei.csv | tr \; '\t'
```

tr mit Zeichenbereiche
```bash
tr '[a-z]' '[A-Z]' < gedicht.txt
```

Löschen mit tr, Leerzeichen und Newline-Zeichen werden einfach hintereinander geschrieben
```bash
tr -d ' \n' < gedicht.txt
```


mehrfache gleiche zeichen mit einem zeichen ersetzen mit tr -s
```bash
tr -s ' ' ' ' < datei.txt  #mehrfache Leerzeichen durch eins ersetzen
```

#Zeichenlänge eines Strings mit awk
```bash
echo $zeichen | awk '{print length("$zeichen")}'
```


Zeichenkette ersetzen mit sed
```bash
echo $zeichenkette | sed 's/sie/die Erde/g'
```bash


Strings ausschneiden 
```bash
echo ${zeichenkette:3:6}
```


Umwandlung von Groß- und Kleinbuchstaben
```bash
name"Marx"
echo ${name^} #ersten Buchstaben groß schreiben
echo ${name^^} #alle Buchstaben groß schreiben
```


## 2.4 Quotings und Kommando-Substitution

Quoting
```bash
echo "das ist eine Variable $var" #Doppelquotes schließen alles aus außer $, Back-Quote und Backslash
echo 'das ist eine Variable $var' #Singlesquotes schließen alles aus
```


Sonderfunktion des Leerzeichens aufgeben (Trennzeichen zwischen Kommandos)
```bash
echo Mehrere    Leerzeichen    werden geloescht
echo "Jetzt bleiben     mehrere Leerzeichen erhalten"
echo 'Jetzt bleiben     mehrere Leerzeichen erhalten'
```

Kommando-Substitution mit Backquotes
```bash
echo "Heute ist `date +%A`"
```

für Bash, Korn und Z-Shell: Kommando-Substitution $()
```bash
echo "Heute ist $(date +%A)"
```

## 2.5 Arrays

Zugriff auf Element eines Arrays
```bash
${variable[x]}
```

Wert zuweisen, Deklaration vorher nicht notwendig, aber empfohlen
```bash
array[3]=drei
```

array für Integerwerte deklarieren
```bash
typseset -i array
```

bei der bash beginnt ein array bei 0, bei z-shell z.B. nicht
```bash
array[0]=null
```

Liste von Werten zuweisen, Leerzeichen fungiert als Trennzeichen
```bash
array=(null eins zwei drei)
```

Alle Elemente eines Arrays ausgeben, Unterscheid zwischen $* und $@ wird in Kapitel 3 erklärt
```bash
echo ${array[*]}
echo ${array[@]}
```

Anzahl eines Arrays
```bash
echo ${#array[*]}
```

Länge eines Eintrags
```bash
echo ${#array[1]}
```

Ab Bash-Version 4.2 und Z-Shell auch negative Indizies möglich
```bash
echo ${#array[-1]} #Inhalt der letzten Zeile
```

array komplett löschen
```bash
unset array
```

einzelnes element löschen
```bash
unset array[2]
```

komplettes array kopieren in bash, in korn- und z-shell anders! (S. 157 - 158
```bash
array_kopie=(${array_quelle[*]}
```

komplettes array kopieren
```bash
Alternative: mit schleife jedes einzelne Element kopieren
```

Assoziative Array, Strings als Index
```bash
NAME[Marx]=Karl
```

```bash
SYMBOL[TRADEMARK]='\u2122' #unicode Zeichen in Array speichern
```


##2.6 Variablen exportieren 

Variable in andere Shell übertragen
```bash
variable=test
export variable
./shellskript_dass_variable_kennt.sh
```

möchte eine Subshell die Variable einer Elternshell verändern, ist dies so nicht möglich
Lösung: Skript mit Punktkommando in Shell ausführen
```bash
. ./skript_laueft_in_shell
```

bei Kommando-Substitution und Gruppierung von Befehlen werden auch alle 
Variablen der Eltern-Shell übergeben (ohne export)

Variable an Subshell vererben mit typeset
```bash
typeset -x variable
```

exportiertr Variablen ansehen
```bash
export 
```

## 2.7 Umgebungsvariablen eines Prozesses

ins Home-Verzeichnis wechseln
```bash
cd
```

## 2.8 Shell-Variablen

#vollständig ab S. 169

Array mit allen Exit-Codes der in einer Pipe ausgeführten Kommandos
```bash
echo $PIPESTATUS
``` 
 
## 2.9 Automatische Variablen der Shell

Name des Shellskripts
```bash
echo $0
```

aktuelle Prozessnummer
```bash
$$
```

Beendigungsstatus des zuletzt ausgeführten Kommandos
```bash
$?
```

Beendigungsstauts des zuletzt gestarteten Hintergrundprozesses 
```bash
$!
```

Automatische Variablen mit wechselnen Inhalten
```bash
LINENO #aktuelle Zeilennummer des Skripts
```
```bash
RANDOM #PSEUDO-Zufallszahl
```
























































