---
title: "Gauge-Taiko UI Testautomatisierung"
date: 2021-10-17T17:17:23+02:00
draft: false
---
Gauge und Taiko bilden eine effiziente Kombination zur UI Automatisierung mit vielen Vorteilen:

Gauge
-----

Gauge ist ein freier Test-Runner, dass es erlaubt lesbare und wiederverwendbare Tests in Markdown format zu schreiben

* Test-Szenario ist Gleichzeit auch der Report
* Testbausteine wiederverwendbar
* Lesbare Tests mit Markdown (ähnlich wie Cucumber)
* Kontrolle der ausgeführten Tests durch Tagging
* Scallierbarkeit
* Datengetriebene Test Möglichkeit

Taiko
-----

Taiko ist eine offene Node.js Bibliothek mit einer einfachen API um automatisiert Browser getriebene Tests in JavaScript zu schreiben.

* Headless browser Tests
* Intelligente Identifizierung von Web-Elementen
* Implizite Warte-Funktionen

Installation
------------

### Vorbedingungen

[node.js](https://nodejs.org) installation ist Voraussetzung.

Für Mac kann es einfach über [Brew](https://brew.sh) installieren:

`brew install node`
                                    

Falls [Brew](https://brew.sh) nicht installiert ist, kann es mit folgenden Befehl installiert werden:

`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
                                    

Die Installation für Windows kann über die offizielle node.js Webseite https://nodejs.org/ getätigt werden.  

### Gauge & Taiko installieren (Mac & Win)

`# Taiko Installation
npm install -g taiko
# Mit -g wird wird die Installation global getätigt
# Check ob es geklappt hat
taiko --version

#Gauge Installation
npm install -g @getgauge/cli`
                                    

VSC & Gauge Plugin

Es gibt für Gauge mit Taiko (und JS) nur ein [VSC Plugin](s://marketplace.visualstudio.com/items?itemName=getgauge.gauge) .

Deshalb die Empfehlung in dieser Kombination mit [Visual Studio Code](https://code.visualstudio.com) zu installieren.

Erstes Taiko-Script aufzeichnen
-------------------------------

Terminal öffnen und folgendes Eintragen:

`#Taiko Starten
taiko`
                                    

Es öffnet sich Taiko und ab hier gibt man nacheinander folgende Taiko [Befehle](https://docs.taiko.dev/api/reference/) zur Testausführung ein

`//Browser öffnen
openBrowser()

//Navigation zur qualitycluster.de Seite
goto("qualitycluster.de")

//click auf wer wir sind
click("Wer wir sind?")

//click auf Manifesto
click("Manifesto")

//Highlight Bereich: Manifesto
highlight("Manifesto")

//Browser schliessen
closeBrowser()`
                                    

Durch die Befehle werden die klicks für den Test aufgezeichnet.

Um nun aus der Click-Abfolge den Taiko-Skript zu generieren kann man mit

                                        `.code`
                                    

den skript generieren.

Nun kann einfach eine js Datei generiert und Taiko geschlossen werden

`// erzeugt eine taikoscript.js Datei mit der aufgezeichneten Abfolge
.code taikoscript.js

//Beenden von Taiko
.exit`
                                    

Jetzt liegt die Skript-Datei vor und kann mit folgenden Befehl ausgeführt werden:

`//Ausführen von taikoscript.js mit Taiko in headfullmode
taiko taikoscript.js --observe`
                                    

Durch das eingeben von „–observe“ wird der Script im sogenannten headfull modus ausgeführt. Dabei wird der Browser physisch geöffnet und auf dem Desktop kann die Ausführung wahrgenommen werden. Ohne diesen Absatz wird ein headless modus ausgeführt, der nicht sichtbar ist, jedoch genau so ausgeführt wird.

**Troubleshooting Ausführungsrichtlinie für Windows Terminal:**

[Siehe Erläuterungsseite Windows](https://docs.microsoft.com/de-de/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.2)

Die Fehlermeldung:

`taiko .\taikoscript.js --observe

taiko : Die Datei "C:\Users\<user>\AppData\Roaming\npm\taiko.ps1" kann nicht geladen werden, da die Ausführung von Skripts auf diesem<br>System deaktiviert ist. Weitere Informationen finden Sie unter "about_Execution_Policies"<br>(https:/go.microsoft.com/fwlink/?LinkID=135170).In Zeile:1 Zeichen:1`
                                    

Lösung: Problem lässt durch setzen der Ausführungsrichtlinien (Execution Policy) für PowerShell-Scripts über GPO lösen

`Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` 
                                    

Ersten Gauge-Taiko script erzeugen
----------------------------------

Nun kommen wir zurück zum VSC und unseren ersten erzeugten leeren Skript.

Neues Projekt einrichten
------------------------

1.  VS Code Starten
2.  CMD + Schift + P drücken und „gauge“ eintippen
3.  „Gauge: Create a New Gauge Project“
4.  Auswahl von „js Template“
5.  Ordner auswählen
6.  Namen eingeben

![](../gauge_vsc.gif)

Ein neues Projekt ist jetzt eingerichtet.

![](../gauge_struktur.png)

Es gibt für den Anfang zwei wichtige Ordner:

specs – Beinhaltet die Spec-Dateien in Markdown die sowohl den Testlauf beschreiben als auch dazu später dienen um den Testreport zu generieren

tests – dort werden alle java script code Dateien abgelegt

Wie man sieht gibt es bereits ein generiertes Beispiel-Test unter specs/examples.spec –> diesen Öffnen

Klick auf Run Scenario lässt den Script laufen

![](../gaugetaiko_runscenario.png)

Nach durchlaufen des Tests wird ein Testreport generiert. Mit ein klick auf das Ergebnis wird dieser geöffnet.

![](../gaugetaiko_runvsc.png)

<– Klick darauf (ist ganz unten zu finden)

Es öffnet Sich der Testreport, darin eine Übersicht über alle ausgeführten Tests. Klick auf das ausgeführte Test.

![](../gaugetaiko_report.png)

Es öffnet sich eine detaillierte Ansicht der Test Ausführung

![](../gaugetaiko_detalierteansicht.png)

Einen ersten kleinen Test schreiben
-----------------------------------

Rechtsklick auf dem Ordner **specs** und neue Datei erstellen. Diese Datei z.B. test.spec benennen.

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-20.52.48.png)

Füge folgenden Text in die neue Datei ein

`# Überschrift des ersten Gauge-Taiko Test

Hier kann man verschiedene Informationen einfügen

Dieser Schritt wird für jeden Test ausgeführt
* Die Seite "qualitycluster.de" öffnen

## Erster Test
* click auf "Wer wir sind?"
* click auf "Manifesto"
* Highlight den Bereich: "Manifesto"`
                                    

Man sieht die Befehle im Testplan sind noch alle rot unterstrichen

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.04.57.png)

Nun Kopiert die erzeugte Datei taikoscript.js in den Ordner tests

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.06.54.png)

Nun kommen die letzten Anpassungen. Wenn man mit der Maus über die rot unterstrichenen Sätzen hält erscheint eine kleine Lampe. Diese Anklicken.

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.08.33.png)

Klick auf „Create step implementation“

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.08.46.png)

Dann die eben kopierte Datei taikoscript.js auswählen

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.08.56.png)

So ung sollte der Inhalt der Datei aussehen:

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.12.10.png)

Dieser teil ist gerade erzeugt wurden durch den VSC-Plugin

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.13.17.png)

Jetzt kann man aus der Aufzeichnung die Funktion selbst übernehmen und in die erstellte Funktion einfügen.

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.13.29.png)

Am ende sollte die Funktion so aussehen.

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.13.59.png)

Der generierte „arg0“ kann durch ein geeigneten Parameter Namen ersetzt werden und wiederum in die Funktion übergeben.

`
step("Die Seite <url> öffnen", async function(url) {
    await goto(url);
});`
                                    

Am ende kann der Ablauf teil gelöscht werden (Achtung die erste Zeile muss bleiben)

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.21.13.png)

So sollte es aussehen:

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.21.52.png)

`const { openBrowser, goto,highlight, closeBrowser } = require('taiko');

step("Die Seite <url> öffnen", async function(url) {
    await goto(url);
});

step("click auf <name>", async function(name) {
    await click(name);
});

step("Highlight den Bereich: <name>", async function(name) {
    await highlight(name)
});` 
                                    

Und damit verschwindet die rot unterstrichenen stellen und der Test kann ausgeführt werden.

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.23.13.png)

Wie man sieht musste der Step * click nur einmal erzeugt werden. Wenn man einen weiteren Satz mit * click beginnt kann man dann diese Funktion für andere Steps nutzen

![](https://qualitycluster.de/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-24-um-21.26.23.png)

Ein beispiel Projekt findet sich unter: [https://github.com/qualitycluster/gauge-taiko](https://github.com/qualitycluster/gauge-taiko)

* * *
