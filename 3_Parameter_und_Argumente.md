## 3.3 Besondere Parameter 


Variable $*
enthält alle Argumente der Kommandozeile als einzelne Zeichenkette
```bash
echo $*
```

iteriere über parameter
```bash
for i in $*
do
	echo '$*:' $i
done
```


werden Argumente in Anführungszeichen übergeben, trennt die for-Schleife
trotzdem die Argumente auf, wegen der Shell-Variable IFS
kommando "mehrere paratemer in anfuehrungszeichen"


iteriere über parameter, diesmal wird $* in Anführungszeichen gesetzt,
Resultat: for-Schleife wird nur einmal durchlaufen, alle Parameter werden gleichzeitig ausgegeben, weil Trennung
mit IFS aufgehoben
```bash
for i in "$*"
do
	echo '$*:' $i
done
```

Unterschied $* und $@
$* ist ein String,  $@ ist ein Array

Siehe: https://unix.stackexchange.com/questions/129072/whats-the-difference-between-and


Variable $#
Anzahl der Argumente


#falls weniger als zwei Argumente übergeben wurden, exit 1
```bash
if [ $# -lt 2 ]
	exit 1
fi
```

## 3.4 Der Befehl shift 


Befehl shift
Schiebt Positionsparameter $1 bis $n jeweils um einen nach links
```bash
shift
```

Schiebt Positionsparameter $1 bis $n jeweils um n nach links
```bash
shift n
```



## 3.5 Argumente und Leerzeichen 

Ein Argument mit einen Leerzeichen übergeben
```bash
kommando argument1 argument2 "Argument3 mit Leerzeichen"
```


## 3.7 Argumente setzen mit set und Kommando-Substitution


Argumente expizit an Positionsparameter übergeben mit set
```bash
set test1 test2 test3
```

Anwendungsbeispiel, set wird vor allem verwendet zur Zelegung und Zuweisung von Zeichenketten
```bash
set $(date)
echo "$3.$2.$6 um $4"
```



## 3.8 getopts - Kommandozeilenoptionen auswerten 

getopts ist ein Kommando, welches sich für eigene komplexere Scripts verwenden lässt, bei
denen Parameter, Argumente und zusätzliche Optionen übergeben werden können

(siehe S. 196)

## 3.9 Vorgabewerte für Variablen (Parameter-Expansion)###


Beispiel-script: lsdirs

#entweder directory bekommt wert von $1 oder, falls nicht gesetzt, Standartwert pwd
```bash
directory=${1:-'pwd'}

ls- ld | grep ^d
```

Weitere Infos ab S. 198



## 3.10 Substring-Expansion


Teilbereiche aus Variable ausschneiden

```bash
${Variable:Position:Länge}
```














































