***

[<< zurück](02_toc.md)

***

# 5.3. Normalisierte Datenstruktur
Spaltenorientierte Datenbanken bevorzugen eine denormalisierte Datenstruktur,  Wenn wir zum Beispiel in einer zeilenorientierten Datenbank ein Kundensystem für ein Zeitungsabonement abbilden wollen haben, wir eine Tabelle für alle Kunden die eine bestimmte Form von Abo haben. Es gibt “Premium, Student, Test”. Dann gibt es eine Tabelle mit den registrierten Kundendatensätzen, eine Tabelle mit der Auflistung welcher Kunder welches Abo seit wann hat und wie lang es läuft und dann vielleicht noch eine Tabelle, welche Einkäufe zusätzlich zum Abo gemacht wurden. Die Tabellen 2-4 in diesem Abschnitt zeigen die zum Beispielfall gehörigen Datenbanktabellen. Die Tabellen sind vereinfaacht dargestellt und würden in der Praxis eher noch Referenzen zu Geodatenbanken haben, für unser Beispiel reichen aber jeweils eine Tabelle mit Kundendaten, den angebotenen Aboformen und der Zuordnung welcher Kunde welches Abo hat über die jeweiligen IDs.


 _Skizzenhafter Aufbau für das Beispiel eines Zeitungsabos in einem zeilenorientierten Datenbanksystem:_


|_kundenId | Name    | Vorname |   Adresse             | Abostart     |
|----|---------|---------|-----------------------|--------------|
| 1  | Müller  | Karl    | Schubertstr. 12       |  12.01.2018  |
| 2  | Schmidt | Otto    | Südring 23	         |  05.11.2018  |
| 3  | Krenz   | Melanie | Am Ring 34	         |  01.05.2018  |
| 4  | Pax     | Anna    | Stadelhofferstr. 13   |  08.05.2018  |

Tabelle 2: Beispiel Kundentabelle für Anwendungsfall "Zeitschriften Abo"



|_aboId |Beschreibung	|Laufzeit in Monaten|   
|----|--------------|-------------------|
| 1 |	Test		| 3 |
| 2 |	Student		| 6 |
| 3 |	Premium		| 12|

Tabelle 3: Beispiel Abonementtabelle für Anwendungsfall "Zeitschriften Abo"


|kundenId | aboId|
|---|---|
|1	|2|
|2	|1|
|3	|3|
|4	|2|
|5	|2|

Tabelle 4: Beispiel Zuordnungstabelle von Kunden zu Abonement





In einer spaltenorientierten Datenbank könnte eine einzige Tabelle die Informationen mit den Kundendaten und den Einkäufen abbilden.
Die Normalisierung der Daten macht es in zeilenorientierten Datenbanken schneller Daten zu aktualisieren, da man dann beim Aktualisieren von Kundendaten nur an einer Stelle ändern muss und alle anderen Transaktionen beziehen sich die Aktualisierung aus der einen Zelle. In der spaltenorientierten Datenbank würde man die KUndendaten zusammen mit den zusätzlichen Einkäufen speichern und müsste dann um bspw. Die Adresse zu aktualisieren, an mehreren Stellen die Aktualisierung vornehmen.


Man kann auch in einer zeilenorientierten Datenbank Datenanalysen machen, sie laufen im Zweifel nur langsamer, als sie in einer spaltenorientierten Datenbank brauchen.
Wenn nur einige wenige Felder einer Wide Table Datenstruktur gebraucht werden sind Column Stores das Richtige, sie sollten jedoch nicht für normale Online Transactional Processing (OLTP) verwendet werden.. Will man etwas wie SELECT * FROM TABLE machen, dann ist eine spaltenorientierte Datenbank, bei der alle Tabellenspalten in separate Dateien gespeichert werden nicht geeignet, da man auf unzählige Dateien zugreifen muss um die Abfrage auszuführen. Für Dienste die ONline Analytical Processing (OLAP) Anwendungen unterstützen sollen, bieten Column Stores in Verbindung mit den in Abschnitt 4.4 beschriebenen Kompressionsverfahren eine hohe Performancesteigerung. In [MG15]

Zeilenorientierte Datenbanken sind in der Regel dafür gemacht schnell bestimmte Daten abzurufen und Transaktionen darauf auszuführen, also schreibend auf die Datenbank zuzugreifen. Spaltenorientierte Datenbank wurden entwickelt um schnell analytische Statistiken zu erheben und auf einer großen Menge von spezifischen Daten zu einer Information auszuwerten.

Wenn wir beispielsweise nicht wissen wollen, welche Haustiere Daniel hat, sondern wir wissen wollen welches Haustier die Deutschen am häufigsten haben, dann fragen wir nur die Information Haustiere ab und nicht das Tupel, welches alle Informationen zu Daniel darstellt, nur um dann zu schauen was in der Zelle “Haustiere” steht.






***

[<< Datenstruktur](07-3_normalized_data-structure.md) | [Anwendungsbeispiele >>](08_use_cases.md)

***