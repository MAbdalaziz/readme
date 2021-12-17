# Aktivitätenplanner

Dieses Projekt bietet Ihnen die Möglichkeit Ihre Aktivitäten zu planen.

## Motivation

Jeder hat Aktivitäten und Termine, die manchmal schwierig zu plannen sind, insbesondere wenn sie viel sind.<br>
Deswegen haben wir Ihnen dieses Projekt zur Verfügung gestellt, das Ihnen hilft, Ihre Aktivitäten und Termine einfach zu plannen um nichts zu verpassen.
 
## Eigenschaften 

* mit diesem Projekt könnten Sie neue Aktivitäten in Datenbank ersterfassen und schon vorhandene bearbeiten oder löschen.
* darüber hinaus können Sie auch die gespeicherte oder bestimmte Aktivitäten über Namen oder Datum anzeigen lassen.
* Sie könnten nach Aktivitäten mit beliebigem Namen Suchen, und werden alle Aktivitäten angeziegt, die gleichen oder ählichen Namen haben.
* daneben könnten Sie alle Aktivitäten anzeigen lassen, die ein beliebiges Datum als Start_Zeit haben.
* außerdem können die gespeicherte Aktivitäten in CSV-Datei heruntergeladen werden.

## Voraussetzungen
der Backend-Teil erfordert folgendes:
1. [Node.js](https://nodejs.org) , um Node Package Manager zu benutzen , und Server zu erstellen 
2. [MongoDB](https://www.mongodb.com/download-center/community), Datenbank um Daten zu speichern.

## das Frontend-Teil gebaut mit:
1. [Angular](https://angular.io/)
  
## Installieren
um alle benötigten Modulen des Projekts zu installieren führen Sie bitte<br>
den folgednen Befehl in CMD aus. 
```
npm install
```

## Testen

Das Projekt hat schon eigene Datei mit Test-Funktionen für <b>Backend</b>, die mit folgendem Befehl ausgeführt werden können.

```
npm run test
```
in diesem Fall wird der Test in Testumgebung ausgefüht werden. das heisst bei Lauf des Projekts wird extra Verbindung<br>
mit Datenbank hergestellt, die nur zum Testen benutzt wird.<br>
darüber hinaus gibt es schon im Projekt einen Ordner mit Postmancollecttion, den Sie auch zum Testen von <b>Backend</b> benutzen könnten.

## Wie benutzt man es?
führen Sie zuerst den folgenden Befehl in Backend-Ordner und danach in Frontend-Ordner
```
npm run start
```
nach dem kompilieren des Projekts, wird die API bereits zum Online Benutzen
und erreichbar unter dieser Adresse http://localhost:4200, wenn es keine Verbindung mit Backend (also mit dem Server) gibt, oder Sie haben den Backend-Teil nicht gestartet, funktioniert die API Offline, und speichert alle Änderungen Lokal bis die Verbindung mit Server erfolgreich ist, dann schickt die API diese Änderungen zum Server.<br><br>

dieses Projekt besteht aus Komponenten die unter folgenden Router zu erreichen sind:
<ul>
<li>/index<br></li>
Das ist die Begrüßungsseite.<br><br>

<li>/Listenansicht<br></li>
Das listet alle Aktivitäten sortiert nach Startzeit auf, und die Heutigen Aktivitäten werden in extra Farbe (Gelb) dargestellt<br>
jede Aktivität hat ein Button zum löschen<br><br>

<li>/Detailansicht<br></li>
Das listet alle Aktivitäten sortiert nach Startzeit auf<br>
jede Aktivität hat auch hier ein Button zum löschen und noch andere Buttons für andere Funktionen.<br>
wenn man an Button (erweitern) klickt, wird dann alle Details dieser Aktivität in Felder angezeigt, die bearbeitet werden können.<br>
wenn man die änderungen nach dem Berabeiten zum Server schicken möchte,
klickt man an Button (Aktualisierung) und danach erscheint eine Meldung um zu zeigen, ob der Vorgang erfolgreich war oder nicht.<br>
<b>Achtung:</b> die Felder der Details sind leer, und die Daten der Aktivität sind als <b>placeholder</b> geschrieben. das heisst Sie sollen die Pflicht felder neu füllen. wenn sie ein Feld nicht ändern möchten dann <b> klicken Sie doppelt darauf </b> um dieser Feld mit dem alten Wert automatisch zu füllen. <br><br>


<li>/aktivitaetenAnzahl<br></li>
Das zeigt der Anzahl der vergangenen und der zukünftigen Aktivitäten an in zwei Blöcke.<br>
wenn man an Block klickt, wird automatisch zu einer entsprechenden Liste von den beiden folgenden Listen weitergelietet.<br><br>
<ol>
<li>/fertigeAktivitaeten<br></li>
Das listet die vergangenen Aktivitäten in Blöcke auf, die bearabeitet oder gelöscht werden können.
<li>/zukuenftigeAktivitaeten<br></li>
Das listet die zukünftige Aktivitäten in Blöcke auf, die bearabeitet oder gelöscht werden können.
</ol><br>

<li>/heutigeAktivitaeten<br></li>
Das listet die heutige Aktivitäten in Blöcken auf, die bearbeitet oder gelöscht werden können.<br><br>

<li>Darüber hinaus, gibts unten rechts in allen Seiten ausser Begrüßungsseite, eine Taste, die noch die folgende Funktionen zur Verfügung stellt: <br></li>
<ol><li>Neue Aktivität Erstellen.</li>
nach jeder Erstellungvorgang wird eine Meldung angeziegt, die Response von Server hat. die Response zeigt das Ergebniss von valideren dieser Aktivität.
<li>die Aktivitäten in CSV herunterladen.</li>
<li>Route zu einer Seite, die zum Suchen (nur Online) dient.</li>
in dieser Seite könnte man nach Aktivitäten mit beliebgem Namen oder Datum (als start zeit) suchen.
</ol>
</ul>

## zusätzliche Funktion:
neben der zusätzlichen <b>Funktion der Suche</b>, habe ich Ihnen noch eine Funktion zur Verfügung gestellt, dass Ihnen bei Erstellung einer grossen Mengen von Aktivitäten oder meherer Aktivitäten mit gleichen Daten hilft.
Sie sollen nur eine <b>JSON Datei von zu erstellenden Aktivitäten auswhälen, und danach wird die ganze Datei eingelesen und davon werden Aktivitäten erstellt und zum Server geschickt</b>. falls eine oder mehrerer Aktivitäten nicht richtig valideren konnten, das heisst nicht im Server gespeichert, wird eine Warnung angezeigt.<br>
=> Diese Funktion ist erreichbar in der Komponente von Erstellung neuer Aktivitäten, es gibt ein Input-File Element um die JSON Datei von loaklen Speicher im Rechnen auszuwählen.

**Ein beispiel von JSON Datei:**

```json
[{
        "name": "IT-Tag",
        "beschreibung": "Webentwicklung",
        "startZeit": "2019-10-27 10:00",
        "endeZeit": "2019-10-27 18:30",
        "ort": "Darmstadt, h_da",
        "fertig": false,
        "prioritaet": 1,
        "kategorien": "Informatik",
        "teilnehmer": ["Mohammed", "Danial"]
                                                },
{
        "name": "IT-Tag2",
        "beschreibung": "Webentwicklung",
        "startZeit": "2019-10-28 10:00",
        "endeZeit": "2019-10-28 18:30",
        "ort": "Darmstadt, h_da",
        "fertig": false,
        "prioritaet": 1,
        "kategorien": "Informatik",
        "teilnehmer": ["Mohammed"]
                                                }]

```
## Offline Funktionalität:
diese API ist auch offline funktionsfähig, wenn Sie einen vorgang ausführen
z.B eine vorhandene Aktivität löschen/aktualisieren oder neue erstellen,
wird es geprüft, ob es ein Response von Server gibt. falls es kein Response gibt weil Server ausser Betrieb ist oder zur Zeit keine Internet-Verbindung gibt, speichert die API die Änderungen loakl in <b> [ localstorage von Browser ] </b>und zeigt eine Warnung.
bei nächster Öffnung der Seiten-komponenten (Routen-komponenten), wird es nochmal geprüft,ob es die Verbindung mit Server erfolgreich ist, war das der Fall, schickt dann die Api alle lokale Änderungen zum Server, sonst bleiben die Änderungen lokal behalten bis es Verbindung gibt.
damit Sie immer eine aktuelle Version von den Daten haben, macht die API bei jeder Öffnung und erflogreicher Internet-Verbindung Synchronisation mit dem Server und ersetzt die lokalen alten Daten mit Neuen.
Wenn sie eine Seite von einer Aktivitäten-Liste aufmacht, und gibts keine Verbidung, holt die API die Daten von dem lokalen Speicher.


## Hinweise
* bei Erstellung einer Aktivität müssen alle Pflichtfelder gefüllt werden.
* jede String Eingabe muss mindestens eine Buchstabe haben und
darf unr diese Sonderzeichen enthalten . , _ -
* das Datum muss in diese Format *yyyy-mm-dd hh:mm* sein *z.B. 2019-10-25 13:55*
* das Datum muss gültig sein, das heisst, wenn es das Datum nicht  gibt, dann wird als ungültig betrachtet
*z.B. 2019-09-31* Dieses Daum ist ungültig weil September nur 30 Tage hat.
* Start_Zeit der Aktivität muss natürlich vor Ende_Zeit sein, sonst wird sie als ungültig betrachtet.
* wenn die eingegebene Ende_Zeit vorbei ist, wird die Aktivität nicht akzeptiert.
* wenn die eingegebene Daten bei Erstellung oder Aktualisierung einer Aktivität nicht richtig validieren konnten,
bekommen Sie in Response eine Meldung, die den Fehler beschreibt.


## Autoren
* **Mohammed Abdalaziz**  [stmoabda](https://code.fbi.h-da.de/stmoabda)
