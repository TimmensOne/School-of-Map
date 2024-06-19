# BASISDATEN
Je nach Bundesland unterscheiden sich die Wege, wie man an (digitale) Kartengrundlagen herankommt. Freie Geodaten gibt es in folgenden Bundesländern:
## Bundesländer
| Bundesland               | Portal-Link | LAS | DOP |
|--------------------------|-------------|-----|-----|
| Baden-Württemberg        | x | x |
| Bayern                   | [Portal](https://geodaten.bayern.de/opengeodata/) | [✓](https://geodaten.bayern.de/opengeodata/OpenDataDetail.html?pn=laserdaten) |
| Berlin                   | x | [✓](https://gdi.berlin.de/geonetwork/srv/ger/catalog.search#/metadata/f4a8997d-4dea-382f-aa3a-d452f4bf3943) |
| Brandenburg              | [Portal](https://geoportal.brandenburg.de) | [✓](https://geobroker.geobasis-bb.de/gbss.php?MODE=GetProductInformation&PRODUCTID=d9895ec2-7039-4c0d-914c-a68f227a7069) |
| Bremen                   | x | x |
| Hamburg                  | [Portal](https://geoportal-hamburg.de/geo-online/) | x |
| Hessen                   | [Portal](https://gds.hessen.de/INTERSHOP/web/WFS/HLBG-Geodaten-Site/de_DE/-/EUR/ViewDownloadcenter-Start;pgid=NIZSrncl7gBSRpNPt1AR16YC0000KzS0h89o) | x |
| Mecklenburg-Vorpommern   | x | x |
| Niedersachsen            | x | x |
| Nordrhein-Westfalen      | x | x |
| Rheinland-Pfalz          | x | x |
| Saarland                 | x | x |
| Sachsen                  | [Portal](https://www.geodaten.sachsen.de/) | ✓ |
| Sachsen-Anhalt           | x | x |
| Schleswig-Holstein       | x | x |
| Thüringen                | x | x |


### Bayern
        https://geodaten.bayern.de/opengeodata/
#### Verfügbare Dateien
 - DGM
 - DOM
 - DOP
 - LAS Daten
#### Tipps
LAS einfach per URL für 1km²-Kachel downloaden:
z. Bsp. https://geodaten.bayern.de/odd_data/laser/682_5382.laz (235258 kB)
wobei 682 und 5382 die UTM Koordinaten der südwestlichen Kachelecke sind
am Besten im BayernAtlas (fka BayernViewer) (https://geoportal.bayern.de/bayernatlas/?bgLayer=tk&E=682000&N=5382000)
auf UTM umstellen

### Brandenburg
        https://geoportal.brandenburg.de

### Hamburg: (freie Geodaten)

        https://geoportal-hamburg.de/geo-online/

Frei erhältlich:
- DGM (leider kein DOP)
- Digitale Orthophotos (DOP20) in CIR und RGB, belaubt und unbelaubt
- ALKIS
- DK5

### Hessen (freie Geodaten): 
        https://gds.hessen.de/INTERSHOP/web/WFS/HLBG-Geodaten-Site/de_DE/-/EUR/ViewDownloadcenter-Start;pgid=NIZSrncl7gBSRpNPt1AR16YC0000KzS0h89o
Nicht einfach durchzublicken, Rohdaten nach Landkreisen in unbeschrifteten
Planquadraten verfügbar; es dauert etwas, bis man das richtige Areal gefunden hat.

### Sachsen
        https://www.geodaten.sachsen.de/         
Top Angebot. Nicht immer einfach durchzublicken. Recherche lohnt sich.
Topaktuelle Roh-Digit. Orthophotos (2022), deutlich besser als die alten DOP.
DGM, DOM, LAS-Daten,...


Sächsische LIDAR-Daten:
(von Franz G.)

Warum überhaupt LAS-Daten? Sie ergeben mit OCAD höher aufgelöste Modelle, als die downloadbaren DHM und DGM. Das heißt, kleinere Gräben und Hügel sind deutlich kontrastreicher erkennbar. Aber der flache Untergrund wird etwas unruhiger (z.B hohe Gräser und unebener Boden in Altenberg). Das stört aber kaum. Außerdem kann nur mit LAS-Daten eine Vegetationsgrundkarte (siehe Ende des Kapitels) und Intensitätskarte erstellt werden, mit der ein erster Eindruck über die Dichte der Vegetation gewonnen werden kann. Die Intensitätskarte liefert für mich sehr oft hilfreiche Erkenntnisse (siehe OCAD-Webseite).

Die einzelnen Messpunkte sächsischer LAS-Daten sind nicht ausführlich kategorisiert. Es gibt nur 2+2: 2 Boden, 20 Nicht-Boden, 30 interpolierter Boden, 8 interpoliertes Wasser.

Durch die sehr grobe Kategorisierung erkennt OCAD keine Gebäude, sodass diese oft als Vegetation dargestellt sind. Eine Vegetationskarte ist also vor allem bei Waldkarten sinnvoll. Ein Versuch, mit Lastools (siehe unten) die Häuser zu erkennen und einzupflegen, lieferte nicht besonders zuverlässige Ergebnisse und ist außerdem lizenzfrei nicht optimal nutzbar. Häuser könnten aber als Vektor anders importiert werden (siehe Kap… .).

Bei der Erstellung der Vegetationsgrundkarte müssen Grenzwerte festgelegt werden. Diese sollte man mit kleineren LAS-Dateien (z.B. in 500x500m mit lastile von LAStolls teilen) testen.

Für Altenberg ergaben bei mir folgende Einstellung sinnvolle Ergebnisse:

 
Ein kleines Problem ergibt sich für Interessierte noch:

Die einzelnen Messpunkte sächsischer LAS-Daten sind ja nicht ausführlich kategorisiert. Es gibt 2 + 2 Kategorien:
2 Boden, 20 Nicht-Boden,         30 interpolierter Boden, 8 interpoliertes Wasser.
Die letzten beiden Kategorien werden künstlich berechnet, da es keinen passenden Reflex der Strahlung gab (z.B durch dichte Vegetation, Wellen, Häuser). OCAD “versteht” die Daten inzwischen, sodass alle DHM-Hintergrundkarten erstellt werden können (auch Vegetationsgrundkarte).
Durch eine kleine Veränderung der Kategorisierung lässt sich das Ergebnis noch leicht verbessern (ist aber für ein sinnvolles Ergebnis keinesfalls nötig). Mit Hilfe von Lastools wird die Kategorisierung verändert: 30 → 1; 2 → 2; 8 → 9; 20 → 4. Dazu brauchen wir las2las64 von LAStools (https://rapidlasso.com/lastools/  download → Verzeichnis bin). Einfach las2las64, die gewünschte LAZ-Datei in einen Ordner packen und im gleichen Ordner eine batch-Datei mit folgendem Text erzeugen (Text in Editor kopieren und z.B als Reperatur.bat speichern):
las2las64 -i *.laz -i *.las -change_classification_from_to 20 4 -change_classification_from_to 30 1 -change_classification_from_to 8 9 -odix _rep1248 -olaz

Danach Batchdatei mit Doppelklick ausführen. Es werden alle LAZ- und LAS-Datei in diesem Ordner verändert und als neue Dateien mit Endung “_rep1248” gespeichert. Fertig :)

Importiert man die so erstellte LAZ-Datei in OCAD, sind die Kategorien richtig. Beim Erstellen des DGM sollte Unklassifiziert und Boden einbezogen, also angehakt werden.

Lidar Case Study( Jeff Teutsch, USA):
Using simple ground reclassification to see features in data

https://drive.google.com/file/d/1YjSeqj6JJrq9xWDfGOulqWQ5YtICFA74/view?fbclid=IwAR3quZ0p0Dym7sYExgdQVdfP_td2WpgANg4DNN2eAuDx8paEnFXPee-VxW8_aem_AV9f3kxcpsFmZNYcFbnDSsZK0zDDxGFctm58qRjMYbTYqYjTqJ3aenS2k-er2XLAE1c 
