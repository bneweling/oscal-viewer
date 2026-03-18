README – GS++ Viewer (lokale HTML-Version)

------------------------------------------------------------
ÜBERBLICK
------------------------------------------------------------
Der GS++ Viewer ist ein rein lokales, webbasiertes Anzeige- und Visualisierungstool zur Darstellung von OSCAL-Catalog-Dateien (JSON) im Grundschutz++-Satzschablonenformat.

Der Viewer unterstützt:
- Katalog-Ansicht: Lesbare Darstellung aller Anforderungen inkl. Inhalte/Parts, Metadaten, Tags sowie Beziehungen.
- Graph-Ansicht: Visualisierung von „verwandt (related)“ und „abhängig von (required)“ als Knoten und Kanten.
- Sunburst: Umfang der Praktiken (z. B. GC, ARCH, …) als Anteilsgrafik.
- Balkendiagramm: Anzahl der Anforderungen je Praktik.
- Filter & Volltextsuche: Mehrfachauswahl per Checkboxen (kombinierbar über alle Filter).
- Export to PDF: Druckoptimierte Ansicht der aktuell gefilterten Katalog-Ansicht (Print-to-PDF über den Browser).

Das Tool kann komplett offline betrieben werden. Es ist kein Internetzugriff erforderlich und es werden keine Daten übertragen.


------------------------------------------------------------
SICHERHEIT UND DATENSCHUTZ
------------------------------------------------------------
Der Viewer arbeitet ausschließlich lokal im Browser.
Es werden keine Daten hochgeladen, keine Server kontaktiert und keine externen Ressourcen nachgeladen, sofern D3.js lokal eingebunden ist (./d3.v7.min.js).

Sicherheitsmerkmale (Tool-seitig):
- Keine Netzwerkfunktionen: Im Code werden keine fetch/XMLHttpRequest/WebSocket-Aufrufe verwendet.
- Keine Persistenz durch das Tool: Es werden keine Cookies, kein LocalStorage, kein SessionStorage und keine IndexedDB genutzt.
- Kein Tracking: Keine Analyse- oder Telemetriedaten.
- Keine Codeausführung aus JSON: OSCAL-Inhalte werden als Text angezeigt (keine Script-Ausführung aus den Daten).

Hinweis zum PDF-Export:
- „Export to PDF“ nutzt die Druckfunktion des Browsers (Druckdialog). Das Speichern als PDF erfolgt im Browser („Als PDF speichern“). Auch hierbei wird nichts hochgeladen.


------------------------------------------------------------
INSTALLATION
------------------------------------------------------------
1. Lege folgende Dateien in denselben Ordner:
   - GS++_Viewer.html (oder ein anderer Name der Viewer-Datei)
   - d3.v7.min.js
   - viewer_logo.png (optional, falls Logo-Anzeige im Viewer gewünscht)
3. Öffne die HTML-Datei per Doppelklick oder per Rechtsklick → „Öffnen mit“ → Browser (z. B. Chrome, Edge oder Firefox).


------------------------------------------------------------
NUTZUNG
------------------------------------------------------------
1. Katalog laden
   Unter „OSCAL Catalog JSON laden“ die gewünschte OSCAL-Catalog-JSON-Datei auswählen.
   Die Datei wird nur lokal eingelesen und nicht übertragen (generell ist jeder Katalog kompatibel, welcher sich an das GS++-Satzschablonenformat hält).

2. Filter (Mehrfachauswahl) & Volltextsuche
   - Praktiken, Quellkataloge, Sicherheitsniveaus, Zielobjekte und Tags sind als aufklappbare Filter verfügbar.
   - In jedem Filter können mehrere Werte per Checkbox gewählt werden.
   - Der Eintrag „Alle …“ (mit Checkbox im Dropdown) markiert bzw. entfernt alle Einträge des jeweiligen Filters.
   - Spezialfilter:
     * Zielobjekte: „Ohne Zielobjekt“ zeigt Anforderungen ohne zugewiesenes Zielobjekt.
     * Tags: „Ohne Tags“ zeigt Anforderungen ohne Tags.
   - Volltextsuche filtert zusätzlich innerhalb der aktuellen Filterung (z. B. nach Begriffen aus Titel/ID/Text/Tags).
   - „Filter zurücksetzen“ setzt alle Filter wieder auf „alles ausgewählt“ und leert das Suchfeld.

3. Katalog-Ansicht
   - Zeigt jede Anforderung vollständig (inkl. Parts/Inhalte), sortiert unter die dazugehörigen Themen und Praktiken.
   - Metadaten pro Anforderung:
     * UUID
     * Quellkatalog/Herkunft (aus „class“)
     * Sicherheitsniveau (aus „sec_level“)
     * Stufe
     * Zielobjekt(e) (aus „target_objects“, sofern vorhanden)
     * Tags (aus „tags“, sofern vorhanden)
   - Beziehungen unterhalb der Anforderung (eingedrückt):
     * Verwandt (related): dunkelgrau hinterlegt
     * Abhängig von (required): dunkel-orange hinterlegt
   - Parameterersetzungen:
     * Platzhalter im Text werden aus „params“ (label) ersetzt und in gelber Schrift innerhalb {{ … }} hervorgehoben.

4. Graph-Ansicht
   - Visualisiert Anforderungen als Knoten und Beziehungen als Linien:
     * related
     * required
   - Die Darstellung orientiert sich an der aktuellen Filterung.
   - Zoom (Mausrad/Trackpad) und Verschieben (Drag) werden unterstützt.

5. Sunburst und Balkendiagramm
   - Sunburst: Anteil je Praktik (größerer Anteil = mehr Anforderungen in der Praktik).
   - Balkendiagramm: Anzahl der Anforderungen je Praktik, beschriftet.

6. Export to PDF
   - Button „Export to PDF“ (unter der Legende) erstellt eine druckoptimierte Ansicht der Katalog-Ansicht.
   - Für den Export im Druckdialog „Als PDF speichern“ wählen.
   - Es werden ausschließlich die aktuell gefilterten Anforderungen exportiert.


------------------------------------------------------------
TECHNISCHE BASIS
------------------------------------------------------------
- Programmiersprache: HTML + JavaScript (Client-side im Browser)
- Bibliothek: D3.js (lokal eingebunden, Version 7.x) für Graph/Sunburst/Balkendiagramm
- Kompatibilität: aktuelle Versionen von Chrome, Edge und Firefox
- Keine Installation notwendig (nur HTML + lokale d3.v7.min.js)


------------------------------------------------------------
FEHLERBEHEBUNG
------------------------------------------------------------
| Problem                            | Ursache                                         | Lösung                                                       |
| ---------------------------------- | ----------------------------------------------- | ------------------------------------------------------------ |
| Es wird nichts angezeigt           | JSON ungültig oder kein kompatibles Format      | Prüfen, ob es ein OSCAL-Catalog im erwarteten GS++-Format ist |
| Graph/Sunburst/Balkendiagramm leer | D3 fehlt oder blockiert                         | d3.v7.min.js im selben Ordner ablegen (./d3.v7.min.js)       |
| Keine Ergebnisse                   | Filter/Suche zu restriktiv                      | „Filter zurücksetzen“ nutzen oder Filter lockern             |
| Export to PDF macht nichts         | Browser blockiert Druckdialog oder Fokusproblem | Erneut klicken; ggf. Tab „Katalog“ aktiv lassen; Browser-Druckfunktion prüfen |
| JavaScript gesperrt                | Unternehmensrichtlinie                          | Viewer kann im Browser dann nicht ausgeführt werden          |


------------------------------------------------------------
EMPFEHLUNG FÜR DEN BEHÖRDEN- ODER UNTERNEHMENSBETRIEB
------------------------------------------------------------
- Viewer und d3.v7.min.js in einer internen Dateiablage bereitstellen.
- Optional: Integritätsprüfung per Hashwert (z. B. SHA-256) dokumentieren.
- Keine Verbindung zu externen Domains erforderlich.
- Ausführung ist ohne Administratorrechte möglich (abhängig von lokalen Richtlinien).


------------------------------------------------------------
LIZENZ
------------------------------------------------------------
3.js steht unter der BSD-3-Lizenz (siehe https://github.com/d3/d3/blob/main/LICENSE).
Die Nutzung/Weitergabe des Viewer-Codes richtet sich nach den Vorgaben Ihrer Organisation bzw. des jeweiligen Repositories.
