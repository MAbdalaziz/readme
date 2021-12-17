# Wetterdienst-System

Dieses Projekt simuliert ein verteiltes System vom Wetterdienst.
 
## Eigenschaften 

* Es gibt zwei Anwendungen, die Sensoren simulieren, eine für Temperatur und eine für Windgeschwindigkeit.
* Diese beiden Sensoren erzeugen jede Sekunde zufällige Daten und senden sie an zwei Themen "Topics", die von zwei Wetterstationen abonniert werden
* Die zwei Wetterstationen verarbeiten die empfangenen Daten, speichern sie in Datenbanken und stellen sie auch über REST Schnittstellte zur Verfügung.
* Die Wetterstationen erstellen auch Berichte aus den von den Sensoren gesendeten Daten und stellen diese auch über REST im PDF- und JSON-Format bereit.
* Über REST können alle gespeicherten Daten oder Daten vom aktuellen Tag oder bis zur letzten Stunde abgefragt werden.
* Neben den Sensoren und zwei Wetterstationen gibt es auch einen Wetterdienst, der abwechselnd eine Anfrage an Wetterstationen sendet, um sich nach den Berichten zu erkundigen und diese über den REST bereitzustellen.
* Für den Fall, dass eine Wetterstation außer Betrieb geht, übernimmt die andere ihre Mission.
* Für den Fall, dass zwei Wetterstationen außer Betrieb gehen, stellt der Wetterdienst über REST den letzten erhaltenen Bericht zur Verfügung und versucht, neue Anforderungen an die beiden Wetterstationen zu verschieben.
* Im Wetterdienst gibt es ein Instrumententafel "Dashboard", in dem die Anzahl der erfolgreichen Abfragen sowie die Anzahl der nicht erfolgreichen Abfragen und andere Informationen angezeigt werden.
* Es gibt auch einen Server, der für die Kommunikation zwischen den Wetterstationen und dem Wetterdienst verantwortlich ist und über den sie ihre Leistung und Probleme überwachen können.

## Voraussetzungen
1. [ActiveMQ](https://activemq.apache.org/components/classic/download/) , um Daten von den Sensoren an Wetterstationen zu senden.
2. [MongoDB](https://www.mongodb.com/download-center/community), Datenbank um Daten zu speichern.

## Installieren
- Machen Sie bitte "Clone" fürs Projekt.
- Importieren Sie bitte das Projekt in IDE.
- Laden Sie bitte MongoDB herunter und installieren Sie es.
- Laden Sie bitte Active MQ herunter.
- Entpacken Sie Active MQ in Ordner <b>src/main/resources/</b> von der Anwendung <b>weather_station_1</b>, sodass Active MQ unter dem Ordner <b>src/main/resources/apache-activemq-5.15.12-bin</b> erreichbar ist.
- Sollten Sie Active MQ woanderes entpacken, Sollten Sie den Pfad in der Datei <b>FirstWeatherstationApplication.java</b> in der Anwendung <b>weather_station_1</b> anspassen.

## Wie benutzt man es?
Führen Sie alle Main-Funktionen der Anwendungen aus, vorzugsweise beginnend mit dem <b>AdminAndDiscoveryServer</b> und gefolgt von der <b>weather_station_1</b>.

Ersetzen Sie die Portnummer in den folgenden Abfragen:<br>
<b>PORT: 9091 für Wetterstation 1</b> <br>
<b>PORT: 9092 für Wetterstation 2</b>
<ul>
<li>Alle Daten, die von Sensoren an Wetterstation gesendet wurden <br></li>
GET localhost:PORT/data/all/<br><br>

<li>Die heutigen Daten, die von Sensoren an Wetterstation gesendet wurden <br></li>
GET localhost:PORT/data/today/<br><br>

<li>Die Daten, die von Sensoren in der letzten Stunde an Wetterstation gesendet wurden <br></li>
GET localhost:PORT/data/lastHour/<br><br>


<li>Die Daten, die vom Temperature-Sensor in der letzten Stunde an Wetterstation gesendet wurden <br></li>
GET localhost:PORT/data/TemperatureLastHour/<br><br>

<li>Die Daten, die vom Windgeschwindigkeit-Sensor in der letzten Stunde an Wetterstation gesendet wurden <br></li>
GET localhost:PORT/data/WindSpeedLastHour/<br><br>

<li>Der Bericht, der von den Temperature-Daten in der letzten Stunde in Wettersatation erstellt wurde (JSON Format)<br></li>
GET localhost:PORT/data/report/temperature/<br><br>

<li>Der Bericht, der von den Windgeschwindigkeit-Daten in der letzten Stunde in Wettersatation erstellt wurde (JSON Format)<br></li>
GET localhost:PORT/data/report/windspeed/<br><br>

<li>Der Bericht, der von den Temperature-Daten in der letzten Stunde in Wettersatation erstellt wurde (PDF Format)<br></li>
GET localhost:PORT/data/report/pdf/temperature/<br><br>

<li>Der Bericht, der von den Windgeschwindigkeit-Daten in der letzten Stunde in Wettersatation erstellt wurde (PDF Format)<br></li>
GET localhost:PORT/data/report/pdf/windspeed/<br><br>

<hr>

<li>Die letzte Berichte, die der Wetterdienst von den Wetterstationen erhalten hat (JSON Format)<br></li>
GET localhost:9090/data/reports/<br><br>

<li>Überwachen von den Abfragen, die der Wetterdienst an die Wetterstationen gesendet hat<br></li>
Zunächst GET localhost:9090/hystrix<br>
und danach im ersten Feld <b> localhost:9090/actuator/hystrix.stream </b> eingeben und an Button <b>[Monitor Stream]</b> klicken.<br><br>

<li>Überwachen vom gesamten System<br></li>
GET localhost:8761 <br>
GET localhost:8761/admin<br><br>


</ul>

## Autoren

* **Mohammed Abdalaziz**  [Github Link](https://github.com/MAbdalaziz/)

