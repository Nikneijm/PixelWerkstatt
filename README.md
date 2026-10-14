# PixelWerkstatt

Web-Werkzeug für **Minecraft Bedrock Edition**: Es baut eigene Add-ons (Behavior Pack und Resource Pack) direkt im Browser. Gedacht für Kinder auf dem Android-Tablet (Chrome), läuft aber in jedem modernen Browser.

**Öffnen:** https://nikneijm.github.io/PixelWerkstatt/

## Was man damit machen kann

- **HUD und Anzeige:** Herzen und Hungerleiste durch eigene 9×9-Icons ersetzen (z. B. Banane oder Currywurst). Die Hotbar lässt sich umfärben (Rahmen, Slots, Auswahlrahmen).
- **Custom Items:** Banane und Kirschen (Food), Waffe, Schrotflinte mit Munition, jeweils mit Crafting-Rezept.
- **Items umtexturieren:** Vanilla-Items wie die Diamant-Spitzhacke bekommen eine neue Textur und funktionieren wie vorher.
- **Custom Mobs:** Vogel, Schmetterling, Elefant (zähmbar und reitbar), Schneeeule und Affe. Jeder Mob hat eigene Geometrie (Bones und Cubes), Texturen und Sounds, Spawn-Regeln nach Biom, ein Spawn Egg und eine Loot-Tabelle.
- **Pixel-Editor** mit 3D-Vorschau.

Als Ergebnis entsteht eine `.mcaddon`-Datei (Resource Pack plus Behavior Pack) oder eine `.mcpack`-Datei (nur Resource Pack, „Nur Aussehen“).

## So kommt das Add-on ins Spiel (Android)

1. In der PixelWerkstatt im Tab **Paket** auf **Komplettpaket erstellen** tippen.
2. In der App **Dateien** → **Downloads** die Datei gedrückt halten → **Öffnen mit** → **Minecraft**. Minecraft importiert das Pack.
3. In Minecraft die Welt bearbeiten → **Verhaltenspakete** (Behavior Packs) → das Pack aktivieren. Das zugehörige Resource Pack wird automatisch mit aktiviert.

Gut zu wissen: Ein aktives Behavior Pack schaltet Erfolge (Achievements) in dieser Welt ab. Das Resource Pack allein („Nur Aussehen“) tut das nicht.

## Technik (für alle, die mitlesen)

- Eine einzige `index.html` mit Inline-JavaScript, kein Build-Schritt. Die Packs werden im Browser mit JSZip gebaut und per Download ausgegeben.
- Alle Items und Mobs liegen im Namespace `wb:`. Die Pack-UUIDs bleiben stabil, nur die Pack-Version zählt hoch, damit Minecraft ein vorhandenes Pack ersetzt, statt ein zweites anzulegen.
- Alle Einstellungen, Zeichnungen und Sounds speichert der Browser des Geräts (`localStorage`). Sie liegen nie in diesem Repo.
- Bibliotheken und Schriften liegen lokal in `lib/` (three.js r128, JSZip 3.10.1) und `fonts/` (Pixelify Sans, Rubik). Beim Besuch wird nichts von Fremdservern geladen.
- Das Manifest gibt eine Mindest-Engine-Version (`min_engine_version`) an. Ziel ist jeweils die aktuelle öffentliche Bedrock-Version.

## Hinweise

- **Inoffiziell:** PixelWerkstatt ist ein inoffizielles Fan-Werkzeug. Es wird nicht von Mojang Studios oder Microsoft hergestellt, genehmigt oder unterstützt. „Minecraft“ ist eine Marke von Mojang Studios bzw. Microsoft. *Not an official Minecraft product. Not approved by or associated with Mojang or Microsoft.*
- **Eigene Inhalte:** Alle Bilder in der Seite sind eigene Pixelzeichnungen. Es wird nichts aus Minecraft mitgeliefert.
- **Rechte:** Der Quelltext ist zum Ansehen öffentlich. Kopieren, Verändern und Weitergeben ist ohne Erlaubnis nicht gestattet. Alle Rechte vorbehalten. Die Seite selbst darf jeder benutzen. Für die mitgelieferten Bausteine anderer gelten deren eigene Lizenzen, siehe [THIRD-PARTY-LICENSES.md](THIRD-PARTY-LICENSES.md).
- **Datenschutz:** Diese Seite sammelt keine Daten und setzt keine Tracker oder Cookies ein. Ausgeliefert wird sie über GitHub Pages. Dabei verarbeitet GitHub technisch bedingt die IP-Adresse der Besucher (siehe Datenschutzerklärung von GitHub).
