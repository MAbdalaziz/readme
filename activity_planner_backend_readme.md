# Aktivitätenplaner

Dieses Projekt biete Ihnen die Möglichkeit Ihre Aktivitäten zu planen.

## Motivation

Jeder hat Aktivitäten und Termine, die manchmal schwierig zu plannen sind, insbesondere wenn sie viel sind.<br>
Deswegen haben wir Ihnen dieses Projekt zur Verfügung gestellt, das Ihnen hilft, Ihre Aktivitäten und Termine einfach zu plannen um nichts zu verpassen.
 
## Eigenschaften 

* mit diesem Projekt könnten Sie neue Aktivitäten in Datenbank ersterfassen und schon vorhandene bearbeiten oder löschen.
* darüber hinaus können Sie auch alle gespeicherte Aktivitäten oder nur eine bestimmte Aktivität über ID anzeigen lassen.
* außerdem können die gespeicherte Aktivitäten in CSV-Datei heruntergeladen werden.
* Sie könnten nach Aktivitäten mit beliebigem Namen Suchen, und werden alle Aktivitäten angeziegt, die gleichen oder ählichen Namen haben.
* daneben könnten Sie alle Aktivitäten anzeigen lassen, die vor, nach oder mit beliebigem Datum sind.
* Es kann sein, dass das Wetter für Ihre Aktivität wichtig ist, deswegen haben wir Ihnen zusätzliche Funktion zur Verfügung gestellt,<br>die Ihnen Informationen über aktueller Wetterstatus und Vorhersage über paar nächste Tagen für die Stadt, in der die Ihre Aktivität stattfinden sollte, aus Yahoo-Weather-API gibt.

## Voraussetzungen
1. [Node.js](https://nodejs.org) , um Node Package Manager zu benutzen , und Server zu erstellen 
2. [MongoDB](https://www.mongodb.com/download-center/community), Datenbank um Daten zu speichern.
  
## Installieren
um das Projekt mit allen benötigten Modulen zu installieren führen Sie bitte<br>
den folgednen Befehl in CMD aus. 
```
npm install
```

## Testen

Das Projekt hat schon eigene Datei mit Test-Funktionen die mit folgendem Befehl ausgeführt werden können.

```
npm run test
```
in diesem Fall wird der Test in Testumgebung ausgefüht werden. das heisst bei Lauf des Projekts wird extra Verbindung<br>
mit Datenbank hergestellt, die nur zum Testen benutzt wird.<br>
darüber hinaus gibt es schon im Projekt einen Ordner mit Postmancollecttion, den Sie auch zum Testen benutzen könnten.

## Wie benutzt man es?
1- Starten Sie bitte zuerst das Projekt mit folgendem Befehl
```
npm run start
```
2- nach dem das Projekt gestartet hat, können Sie Projekt-Feautres
mittels einer HTTPAPI folgendes benutzen:

<ul>
<li>alle Aktivitäten anzeigen <br></li>
GET localhost:3001/api/aktivitaet/<br><br>

<li>bestimmte Aktivität anzeigen über ID <br></li>
GET localhost:3001/api/aktivitaet/aktivitaetId<br><br>

<li>bestimmte Aktivität löschen  über ID<br></li>
DELETE localhost:3001/api/aktivitaet/aktivitaetId<br><br>

<li>bestimmte Aktivität aktualisieren  über ID<br></li>
PUT localhost:3001/api/aktivitaet/aktivitaetId<br><br>

<li>neue Aktivität anlegen<br></li>
POST localhost:3001/api/aktivitaet/<br><br>

<li>neue Aktivität anlegen und Informationen über Wetterstatus
für die Stadt bekommen, <br>wo die Aktivität stattfinden sollte<br></li>
POST localhost:3001/api/aktivitaet/getwetter<br><br>

<li>vorhandene Aktivität aktualisieren und Informationen über Wetterstatus für die Stadt bekommen, <br>wo die Aktivität stattfinden sollte<br></li>
PUT localhost:3001/api/aktivitaet/getWetter/aktivitaetId<br><br>

<li>die Aktivitäten in CSV-Datei herunterladen<br></li>
GET localhost:3001/api/aktivitaet/csv/herunterladen<br><br>

<li>nach Aktivitäten mit gleichem oder ähnlichem Namen suchen<br></li>
GET localhost:3001/api/aktivitaet/name/beliebigerName <br><br>

<li>nach Aktivitäten suchen, die vor beliebigem Datum sind<br></li>
GET localhost:3001/api/aktivitaet/vor/beliebigesDatum <br><br>

<li>nach Aktivitäten suchen, die nach beliebigem Datum sind<br></li>
GET localhost:3001/api/aktivitaet/nach/beliebigesDatum <br><br>

<li>nach Aktivitäten suchen mit beliebigem Datum<br></li>
GET localhost:3001/api/aktivitaet/datum/beliebigesDatum <br><br>

<li>Informationen über Wetterstatus in einer Stadt<br></li>
GET localhost:3001/api/wetter/stadtname<br><br>
</ul>

**Die Variablen zur Erstellung oder Aktualisierung einer Aktivität können in Request Body geschickt werden**
z.B.
```json
{
        "name": "IT-Tag",
        "beschreibung": "Webentwicklung",
        "startZeit": "2019-10-27 10:00",
        "endeZeit": "2019-10-27 18:30",
        "ort": "Darmstadt, h_da",
        "fertig": false,
        "prioritaet": 1,
        "kategorien": "Informatik",
        "teilnehmer": ["Mohammed", "Danial"]
                                                }
```

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
* um automatisch informationen über Wetterstatus für die Stadt bekommen,
wo die Aktivität stattfinden sollte, bei Erstellung oder Aktualisierung einer Aktivität,
geben Sie bitte in Ort_Feld **den Stadtnamen gefolgt mit komma** und danach den Rest der Adresse 
*z.B. "ort": "Darmstadt, h_da"*
* sonst wenn es Warnung oder Info gibt, bekommen Sie eine Meldung in Response.

## Autoren

* **Mohammed Abdalaziz**  [Github Link](https://github.com/MAbdalaziz/)
