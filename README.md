# PixelWerkstatt

Web-Werkzeug für **Minecraft Bedrock Edition**: Es baut eigene Add-ons (Behavior Pack und Resource Pack) direkt im Browser, mit eigenem Essen, Waffen und Werkzeugen, Deko-Blöcken, Mobs, Blocktexturen und HUD. Gedacht für Kinder auf dem Android-Tablet (Chrome), läuft aber in jedem modernen Browser.

**Öffnen:** https://nikneijm.github.io/PixelWerkstatt/

## Was man damit machen kann

- **HUD und Anzeige:** Herzen und Hungerleiste durch eigene 9×9-Icons ersetzen (z. B. Banane oder Currywurst). Die Hotbar lässt sich umfärben (Rahmen, Slots, Auswahlrahmen).
- **Essen (Food und Drink):** Banane, Kirschen, Blaubeere, Weintrauben, Nüsse und Trinkglas (bleibt nach dem Trinken erhalten). Füllt die Hungerleiste (im Kreativmodus gibt es keinen Hunger). Apfel und Brot lassen sich umtexturieren.
- **Waffen und Werkzeug:** Waffe, Schrotflinte mit Patronen (jeweils mit Crafting-Rezept), Kastanie zum Werfen (Throwable wie der Schneeball, ohne Schaden) und Drachen zum Fliegen: In der Hand gibt er Slow Falling, beim Benutzen einen Levitation-Stoß nach oben (kleines Skript über die stabile Script API `@minecraft/server`, keine Experimente nötig). Spitzhacken und Schwerter lassen sich umtexturieren und funktionieren wie vorher.
- **Eigene Custom Items:** Im Tab Essen als Food oder Drink, im Tab Waffen & Werkzeug als Waffe, Werkzeug (Spitzhacke, Axt, Schaufel mit `minecraft:digger` und Tool-Tags), Wurf-Item oder Flug-Item. Selbst benennen und bemalen.
- **Deko (Custom Blocks):** Computer, Laptop, Koffer mit Rollen, Palme und Tisch als Blöcke mit eigener Geometrie (`minecraft:geometry`), die sich beim Hinstellen zum Spieler drehen (`minecraft:placement_direction`). Computer und Laptop geben etwas Licht ab. Eigene Deko-Teile aus Grundformen (u. a. Kiste). Farben und Pixel werden wie bei den Mobs gestaltet, mit 3D-Vorschau.
- **Custom Mobs:** Vogel, Schmetterling, Elefant (zähmbar und reitbar), Schneeeule, Affe, Häschen (hoppelt mit `minecraft:movement.skip`), Pfau (mit Rad), Maus und Drache (fliegendes Reittier: tameable mit Fleisch oder Fisch, gesteuert wie der Happy Ghast mit `minecraft:free_camera_controlled` und `minecraft:vertical_movement_action`, nur per Spawn Egg). Jeder Mob hat eigene Geometrie (Bones und Cubes), Texturen und Sounds, Spawn-Regeln nach Biom, ein Spawn Egg und eine Loot-Tabelle.
- **Eigene Mobs:** Neue Mobs selbst anlegen und benennen, auf Basis einer Bauform: Vogel, Schmetterling, Eule, Zweibeiner, Häschen, Maus, Pfau, Reittier, großes Reittier und Drache (tameable und rideable), Fisch und Qualle (Wasser-Mobs mit Unterwasser-Navigation). Biom für die Spawn Rule wählbar, oder nur per Spawn Egg.
- **Blocktexturen:** 621 Vanilla-Block-Sorten (über 1.100 Blöcke inklusive Treppen, Stufen und Mauern) mit Suche. Je Seite umfärben, Muster wählen (körnig, Ziegel, Bretter, Holz, Erz) oder Pixel für Pixel bemalen, mit 3D-Würfel-Vorschau. Die Texturen ersetzen im Resource Pack die Originale.
- **Pixel-Editor** mit 3D-Vorschau.
- **Sounds direkt aufnehmen:** Ruf- und Hurt-Sound jedes Mobs werden direkt auf der Seite über das Mikrofon aufgenommen (MediaRecorder, bis 4 Sekunden, mit Stopp-Knopf) und als WAV (16 kHz, mono) ins Resource Pack gelegt. Eine vorhandene Audiodatei kann weiterhin gewählt werden.
- **Paket-Auswahl:** Anfangs ist nichts markiert. Markiert wird direkt auf jeder Kachel (Häkchen oben rechts), ein ganzer Bereich oder ein ganzer Tab mit „Alle markieren“. Beim Export wählt man „Nur markierte“ (was in den Tabs markiert ist) oder „Alle Elemente“ (alles aus allen Tabs; bei Blöcken alle veränderten Texturen).

Als Ergebnis entsteht eine `.mcaddon`-Datei (Resource Pack plus Behavior Pack) oder eine `.mcpack`-Datei (nur Resource Pack, „Nur Aussehen“).

## So kommt das Add-on ins Spiel (Android)

1. In der PixelWerkstatt im Tab **Paket** wählen, ob **Nur markierte** oder **Alle Elemente** ins Pack sollen, dann auf **Komplettpaket erstellen** tippen.
2. Im Hinweis „Download abgeschlossen“ auf **Öffnen** tippen und **Minecraft** wählen (mit „Immer“ öffnet Android solche Dateien künftig direkt mit Minecraft). Minecraft importiert das Pack. Alternativ in der App **Dateien** → **Downloads** die Datei antippen.
3. In Minecraft die Welt bearbeiten → **Verhaltenspakete** (Behavior Packs) → das Pack aktivieren. Das zugehörige Resource Pack wird automatisch mit aktiviert. Bei „Nur Aussehen“ (`.mcpack`) stattdessen unter **Ressourcenpakete** aktivieren.

Gut zu wissen: Ein aktives Behavior Pack schaltet Erfolge (Achievements) in dieser Welt ab. Das Resource Pack allein („Nur Aussehen“) tut das nicht.

## Technik (für alle, die mitlesen)

- Eine einzige `index.html` mit Inline-JavaScript, kein Build-Schritt. Die Packs werden im Browser mit JSZip gebaut und als `.mcaddon` bzw. `.mcpack` heruntergeladen.
- Alle Items, Mobs und Deko-Blöcke liegen im Namespace `wb:`. Computer, Laptop, Koffer und Palme waren früher Items und sind jetzt Blöcke mit derselben Kennung. Eigene Items, Mobs und Deko-Teile bekommen ihre Kennung einmalig aus dem Namen (z. B. `wb:qualle`); spätere Umbenennungen ändern nur den Anzeigenamen. Die Pack-UUIDs bleiben stabil, nur die Pack-Version zählt hoch, damit Minecraft ein vorhandenes Pack ersetzt, statt ein zweites anzulegen.
- Blocktexturen werden über denselben Pfad wie im Vanilla Resource Pack ersetzt (`textures/blocks/…`, bei Laub auch die `_opaque`-Variante und das Inventarbild). Für die Blockliste enthält die Seite nur Block-Kennungen, die deutschen Blocknamen und die Durchschnittsfarbe der Originaltexturen (ermittelt aus Mojangs öffentlichen `bedrock-samples`, Stand 1.26.50) als Startfarbe. Bilder aus Minecraft werden nicht mitgeliefert.
- Alle Einstellungen, Zeichnungen und Sounds speichert der Browser des Geräts (`localStorage`). Sie liegen nie in diesem Repo. Mikrofon-Aufnahmen werden nur im Browser verarbeitet und nirgendwohin gesendet.
- Bibliotheken und Schriften liegen lokal in `lib/` (three.js r128, JSZip 3.10.1) und `fonts/` (Pixelify Sans, Rubik). Beim Besuch wird nichts von Fremdservern geladen.
- Das Behavior Pack bekommt nur dann ein Script-Modul (`scripts/main.js`, `@minecraft/server` 1.15.0), wenn ein Flug-Item im Pack ist.
- Das Manifest gibt eine Mindest-Engine-Version (`min_engine_version`) an. Ziel ist jeweils die aktuelle öffentliche Bedrock-Version.

## Hinweise

- **Inoffiziell:** PixelWerkstatt ist ein inoffizielles Fan-Werkzeug. Es wird nicht von Mojang Studios oder Microsoft hergestellt, genehmigt oder unterstützt. „Minecraft“ ist eine Marke von Mojang Studios bzw. Microsoft. *Not an official Minecraft product. Not approved by or associated with Mojang or Microsoft.*
- **Eigene Inhalte:** Alle Bilder in der Seite sind eigene Pixelzeichnungen oder werden aus Farben erzeugt. Es werden keine Texturen, Modelle oder Sounds aus Minecraft mitgeliefert. Blocknamen und Durchschnittsfarben dienen nur dazu, die Blöcke im Spiel zuzuordnen.
- **Rechte:** Der Quelltext ist zum Ansehen öffentlich. Kopieren, Verändern und Weitergeben ist ohne Erlaubnis nicht gestattet. Alle Rechte vorbehalten. Die Seite selbst darf jeder benutzen. Für die mitgelieferten Bausteine anderer gelten deren eigene Lizenzen, siehe [THIRD-PARTY-LICENSES.md](THIRD-PARTY-LICENSES.md).
- **Datenschutz:** Diese Seite sammelt keine Daten und setzt keine Tracker oder Cookies ein. Ausgeliefert wird sie über GitHub Pages. Dabei verarbeitet GitHub technisch bedingt die IP-Adresse der Besucher (siehe Datenschutzerklärung von GitHub).
