Benutzernamen ausgeben
```bash
whoami
```

angemeldete Benutzer
```bash
who
```

dauerhaft zum root wechseln
```bash
sudo -i
```

zurück zum letzten Verzeichnis $OLDPWD
```bash
cd -
```

Shellscript ohne Subshell ausführen
```bash
. ./script_zum_ausfuehren
```

letzten exit-status anzeigen
```bash
echo $?
```

Prozessnummer der Shell ausgeben
```bash
echo $$
```

Debug-Variable PS4 austauchen/verbessern
```bash
export PS4="[--- Zeile: ${LINENO} ---] "
```

1.10 Datenstrom 

Standardfehlerausgabe umleiten
```bash
befehl 2>/dev/null
```

Standardfehlerausgabe an Datei anhängen
```bash
befehl 2>> error.log
```

Standardausgabe und Standardfehlerausgabe an Datei anhängen
```bash
befehl > info_and_error.log 2>$1
```

Standardausgabe und Standardfehlerausgabe an Datei anhängen
```bash
befehl &> info_and_error.log  ab Bash Version 4.x
```

Ausgabe mit tee ausgaben und an Datei anhängen
```bash
ls -li | tee -a file.log
```

Wildcard-Zeichen der Shell
```bash
* , ? und []
```

Dateinamen Expansion mit **, alle Dateien ab Verzeichnis rekursiv ansprechen, Option "globstar" muss mit shopt -s globstar gesetzt werden oder dauerhaft in ~/.bashrc (S.98-99)
```bash
ls -l **
```

Eine beliebige Zeichenfolge mit *, z.B.:
```bash
grep Backup /home/tot/Mails/*.txt
```

Ein beliebiges Zeichen mit ?, z.B.:
```bash
ls datei?.dat
```

Zeichenbereich angeben, z.B.
```bash
ls datei[123].txt
```

Zeichenbereich angeben für zwei Zeichen, z.B.
```bash
ls datei[1-4][1-4].txt
```

Zeichenbereich angeben für beliebig viele Zeichen, z.B.
```bash
ls datei[1-4][1-4].txt
```

Debugging-Option 
```bash
set -x
```

vordefinierte Expansionenparameter
```bash
[:alpha:] anstatt [a-zA-Z]
[:digit:] anstatt [0-9]
```

versteckte Dateien bei Datei-Expansion
```bash
ls .*.conf
```

Tilde-Expansion
```bash
~ Heimverzeichnis
~- Verzeichnis, das zuvor besucht wurde
~+ aktuelles Arbeitsverzeichnis pwd
```
















