# CMS-gestützte Microservices-Webanwendung

Dies ist eine Webanwendung, deren Inhalt auf Headless-CMS basiert.

## Eigenschaften

Über diese Anwendung können die folgenden Daten eingegeben, verwaltet und dann in Vorlagen
angezeigt werden:


- Firmenname
- Ein Bild mit einer Willkommensnachricht
- Informationen von Produkten
- Statistiknummern mit einer kurzen Beschreibung
- Text über die Firma
- Informationen von Diensten
- Informationen von Veranstaltungen
- Soziale Medien Links der Firma

## Voraussetzungen
- Java-Laufzeitumgebung (Version 8)
- Docker
- Maven

## Starten


1. Starten Sie bitte Docker
2. Nachdem Docker-Start, führen Sie bitte die Datei namens "install, build and run.bat" aus, die mit
dem Projekt und geliefert wurde.
Nach dem Ausführen der Datei werden alle erforderlichen Vorgänge ausgeführt, vom Herunterladen,
Erstellen usw. zum Ausführen der Anwendungskomponenten.
Acht Konsolen werden in einer Reihe mit einer Pause dazwischen geöffnet.
Sieben Konsolen davon sind für die Komponenten der Anwendung und die achte Konsole ist für MySQL-Docker-Container.
3. Schließlich wird die Anwendungsseite automatisch im Browser geöffnet.



### Achtung:

Wenn ein Fehler auftritt oder die Anwendung nicht ordnungsgemäß ausgeführt wird, stellen Sie sicher,
dass alle Konsolen ordnungsgemäß funktionieren. Manchmal stoppt eine Konsole in Windows und man
muss dann die Eingabetaste drücken, damit Konsole weiter ausgeführt wird. Wenn alle Konsolen
ordnungsgemäß funktionieren und die Anwendung noch nicht funktioniert, warten Sie bitte eine Minute
oder etwas länger, da möglicherweise eine Anwendung vor der anderen funktioniert hat und in diesem
Fall werden die Anwendungen erneut versuchen, miteinander zu kommunizieren.

## Komponenten

### 1) Headless-CMS

- In dieser Komponente kann man über den folgenden Link, der im Browser geöffnet werden kann,
den Inhalt der Anwendung einpflegen:

  - **Link:** http://localhost:8080/cms
  - **Benutzername:** admin
  - **Passwort:** admin


- Die eingepflegten Daten werden über eine REST-Schnittstelle veröffentlicht, auf die über den
folgenden Link zugegriffen werden kann:

   **Link:** http://localhost:8080/site/store/documents/


### 2) Registrierungsservice (Registration Server)

Diese Awendung funktioniert auf **Port 8881**.
Alle Anwendungskomponenten registrieren beim Start ihre Kontaktinformationen bei dieser Awendung,
damit die anderen Komponenten namentlich mit ihnen kommunizieren können.

Im Browser kann man über den folgenden Link alle Anwendungskomponenten sehen, die sich bei
diesem Server registriert haben:
**Link:** [http://localhost:8881/](http://localhost:8881/)

### 3) Gateway

Diese Awendung funktioniert auf **Port 8882**.
Sie ist für die Weiterleitung und Verteilung von Anforderungen an die erforderlichen und verfügbaren
Komponenten sowie für die Überprüfung der Gültigkeit der Anforderungen verantwortlich.


Die Anwendung verwendet eine H2-Datenbank, die die Daten in einer Datei speichert. Auf die
Datenbank kann im Browser über die folgenden Informationen zugegriffen werden:

- **Link:** http://localhost:8882/h2-console
- **JDBC URL:** jdbc:h2:./zuulgatewaydb
- **Benutzername:** admin
- **Passwort:** admin

Die Anwendung enthält eine REST-Schnittstelle für die folgenden Funktionen:

- **Benutzerregistrierung:**
POST http://localhost:8882/api/signup
Der Request-Body soll wie folgt aussehen:
```
{ "username" : "mohammed",
"password" : "password",
"email": "example@mail.com",
"name": "Mohammed Abdalaziz" }
```

Nach einem erfolgreichen Benutzerregistrierungsprozess schickt diese Funktion den Benutzernamen
des registrierten Benutzers zurück.

Beim Start der Anwendung werden zwei Benutzer in der Datenbank gespeichert mit den folgenden
Daten:

**Daten vom Benutzer 1**   Benutzername: admin   Passwort: admin

**Daten vom Benutzer 2**   Benutzername: mo   Passwort: pass

- Anmeldung:
POST http://localhost:8882/api/signin
Der Request-Body soll wie folgt aussehen:
```
{ "username" : "mohammed",
"password" : "password" }
```

Nach einem erfolgreichen Anmeldungsprozess schickt diese Funktion ein JWT zurück.


### 4) Inhaltsanbieter (Content Provider)

Es gibt zwei Instanzen dieser Komponente, die auf die Ports: **8883** und **8884** laufen. Diese Instanzen
senden jede Minute eine GET-Anfrage an das CMS, um die Daten zu holen. Außerdem stellen diese
Instanzen dem Client die aus CMS abgefragten Daten zur Verfügung, die zum Erstellen der Seite


benötigt werden. Alle Daten werden für alle Clients zurückgegeben, mit Ausnahme der Produktdaten, die
entsprechend der Rolle des Clients zurückgegeben werden.
Die Instanzen verwenden eine MySQL-Datenbank (Version 5), die im Docker-Container ausgeführt wird.
Die Verbindung mit einer externen Datenbank ist möglich, indem die Zugangsdaten in der Datei
**"application.properties"** angepasst werden, die sich in beiden Instanzen befindet.

Jeder Instanz enthält eine REST-Schnittstelle mit den folgenden Funktionen:


1. Funktion gibt dem Client die Daten zurück:

   + Direkt aufrufen GET http://localhost:PORT/data
Der Header soll wie folgt eine Rolle enthalten:
        ```
        Header-Key: role Header-Value: premium
        ```
   + Aufrufen über Gateway GET http://localhost:8882/api/contentprovider/data
   Das Gateway fügt den Rolle-Header automatisch



2. Funktion gibt die Daten der Produkte für den Purchase-Service zurück:

   + Direkt aufrufen GET http://localhost:PORT/productsdetails

   + Aufrufen über Gateway GET http://localhost:8882/api/contentprovider/productsdetails
   Der Header soll wie folgt eines von den in der Datei "application.properties" vordefinierten
   Geheimnise für die Kommunikation enthalten:
        ```
        Header-Key: serviceSecret Header-Value: POlikUZttVBcx
        ```
### 5) Kaufservice (Purchase Service)

Diese ist eine zusätzliche Anwendung und funktioniert auf **Port 8885**.
Sie ist für die Kauffunktion verantwortlich und fragt jede Minute die Daten der Produkte vom
Inhaltsanbieter ab. Diese Anwendung verwendet eine H2-Datenbank, die die Daten in einer Datei
speichert. Auf die Datenbank kann im Browser über die folgenden Informationen zugegriffen werden:

- **Link:** [http://localhost:8885/h2-console](http://localhost:8885/h2-console)

- **JDBC URL:** jdbc:h2:./purchaseservicedb

- **Benutzername:** admin

- **Passwort:** admin

Diese Anwendung enthält eine REST-Schnittstelle für die folgenden Funktionen:

1. **Kauffunktion:**
   
    - Direkt aufrufen POST http://localhost:8885/purchase

        Der Header soll wie folgt den Benutzernamen enthalten:
        ```
        Header-Key: username Header-Value: admin
        ```


        Der Request-Body soll die ID das zu kaufenden Produkts wie folgt enthalten:

        ```
        { "productId" : "3" }
        ```

   - Aufrufen über Gateway POST http://localhost:8882/api/purchaseservice/purchase
   Das Gateway fügt den Benutzername-Header automatisch.
   Weil die Kaufkomponente gesichert ist, muss der Header ein JWT enthalten, das mit "Bearer"
   beginnt. Wenn das JWT "xxxxxxxx" lautet, kann der Header wie folgt aussehen:
        ```
        Header-Key: Authorization Header-Value: Bearer xxxxxxxx
        ```


        Der Request-Body soll die ID das zu kaufenden Produkts wie folgt enthalten:
        ```
        { "productId" : "3" }
        ```

        Nach einem erfolgreichen Kaufprozess schickt diese Funktion eine Abrechnung zurück.

2. **Funktion gibt alle Rechnungen für einen Benutzername zurück:**

   - Direkt aufrufen GET http://localhost:8885/shoppinglist

       Der Header soll wie folgt den Benutzernamen enthalten:
       ```
       Header-Key: username Header-Value: admin
       ```

   - Aufrufen über Gateway GET http://localhost:8882/api/purchaseservice/shoppinglist
   Das Gateway fügt den Benutzername-Header automatisch.
   Weil die Kaufkomponente gesichert ist, muss der Header ein JWT enthalten, das mit "Bearer"
   beginnt. Wenn das JWT "xxxxxxxx" lautet, kann der Header wie folgt aussehen:
        ```
        Header-Key: Authorization Header-Value: Bearer xxxxxxxx
        ```

### 6) Client

Die Client-Anwendung basiert auf dem Vue-Framework und ist über den folgenden Link verfügbar, der
im Browser geöffnet werden kann:
**Link:** [http://localhost:10000/](http://localhost:10000/)

Die Anwendung enthält die folgenden Seiten:


- Hauptseite
- Produktseite (die Produkte werden entsprechend der Rolle angezeigt, die der Benutzer besitzt)
- Loginseite
- Neue Benutzerregistrierungsseite
- Kaufenübersichtsseite (wird erst nach einem erfolgreichen Anmeldevorgang angezeigt)

Man kann über die Registrierungsseite ein neues Benutzerkonto erstellen und sich dann auf der
Anmeldeseite damit anmelden. Oder man kann eines der folgenden Konten verwenden:
**Daten vom Benutzer 1**   Benutzername: admin   Passwort: admin

**Daten vom Benutzer 2**   Benutzername: mo   Passwort: pass

## Autoren
**Mohammed Abdalaziz**  [Github](https://github.com/MAbdalaziz)



