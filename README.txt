MASCHENPROBEN-RECHNER ALS PWA (Version 2, mit Banderolen-Scan)

Inhalt dieses Pakets
  index.html              die App
  manifest.webmanifest    App-Beschreibung (Name, Icons, Farben)
  sw.js                   Service Worker (Zwischenspeicher fuer Offline-Nutzung)
  icon-192.png, icon-512.png, icon-maskable-512.png

WAS IST NEU
  Die Garnliste ist weg. Stattdessen fotografiert man die Banderole. Die Texterkennung
  (Tesseract.js) laeuft im Browser auf dem Geraet, es wird kein Foto an einen Server
  gesendet. Die App sucht im erkannten Text nach Laufaenge/Gewicht (z. B. "50 g = 105 m"),
  Nadelstaerken ("3-3,5 mm") und Maschenproben ("22 M x 32 R").
  Erkannte Werte sind Vorschlaege und muessen geprueft werden.

1. Auf eigene Domain hochladen (HTTPS ist Pflicht, sonst gibt es keinen Kamerazugriff
   und keine Installation). Alle Dateien in dasselbe Verzeichnis legen, am besten
   ins Hauptverzeichnis einer (Sub-)Domain.

2. Testen
   Seite in Chrome (Android) oeffnen, Banderole fotografieren, Ergebnis mit dem Etikett
   vergleichen. Unter "Erkannter Text anzeigen" siehst du, was die Texterkennung gelesen hat.
   Lighthouse (Chrome-Entwicklertools) pruefen: PWA-Kriterien.

3. Wichtig: Bibliotheken
   index.html laedt zur Laufzeit:
     pdf.js 2.16.105          von cdnjs.cloudflare.com  (PDF-Anleitungen lesen)
     tesseract.js 5.1.1       von cdn.jsdelivr.net     (Banderolen lesen)
   Tesseract laedt beim ersten Scan zusaetzlich Kern-Datei und Sprachdaten
   (Deutsch und Englisch, einige MB). Danach liegen sie im Zwischenspeicher.
   Fuer echten Offline-Betrieb und mehr Datenschutz kannst du alles selbst hosten:
   tesseract.min.js, worker.min.js, tesseract-core und die Sprachdateien deu/eng
   herunterladen, neben index.html legen und im Aufruf Tesseract.recognize die Optionen
   workerPath, corePath und langPath auf deine Dateien setzen (siehe Tesseract.js-Doku).
   Das konnte ich in dieser Umgebung nicht fuer dich vorbereiten, weil hier kein
   Internetzugriff besteht.

4. Als Android-Paket verpacken (.aab)
   https://www.pwabuilder.com : URL eingeben > Package for stores > Android > Google Play.
   Die Datei assetlinks.json muss unter
   https://deine-domain.de/.well-known/assetlinks.json erreichbar sein.
   Die App braucht Kamera-/Dateizugriff nur ueber die Dateiauswahl des Systems.

5. Google Play Console
   - Entwicklerkonto: einmalig 25 US-Dollar, Identitaetspruefung.
   - Neue private Konten (nach 13.11.2023): geschlossener Test mit mind. 12 Testern ueber
     14 Tage, dann Produktionszugriff beantragen. Organisationskonten sind laut
     aktuellen Quellen ausgenommen. Bitte in der Play Console pruefen.
   - Store-Eintrag, Screenshots, Feature-Grafik (1024x500), Datenschutzerklaerung,
     Data Safety, Altersfreigabe.
   - Datenschutz: Fotos und Texte werden nur im Browser verarbeitet und nicht
     gespeichert oder gesendet (ausser dem Nachladen der Bibliotheken von den CDNs,
     solange du sie nicht selbst hostest). Das gehoert in die Datenschutzerklaerung.

Grenzen
  - Texterkennung ist bei Knitterfalten, Spiegelungen, kleiner oder verspielter Schrift
    unzuverlaessig. Symbole (Nadel-Piktogramme) kann sie nicht deuten: Die erste gefundene
    mm-Angabe wird als Stricknadel, die zweite als Haekelnadel angenommen. Bitte pruefen.
  - Die Claude-Funktionen aus der claude.ai-Version (Foto durch KI lesen) sind in dieser
    Version nicht enthalten.
