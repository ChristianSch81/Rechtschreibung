# AGENTS.md – Vorlage für interaktive Lernpakete

## Zweck

Erstelle eigenständige, browserbasierte Lernpakete im visuellen Stil dieses Projekts. Übernimm das Layoutsystem, die Bedienlogik und die Qualitätsstandards, aber ersetze Fach, Titel, Kapitel, Aufgaben und Bilder durch die Inhalte des jeweiligen Projekts.

Die Anwendung soll ohne Build-Prozess und ohne externe Abhängigkeiten als statische Website funktionieren. Sie muss lokal per `index.html`, auf GitHub Pages und eingebettet in eine Lernplattform nutzbar sein.

## Vor Beginn anpassen

Lege für jedes neue Projekt diese Werte fest:

- `[FACH]`: z. B. Deutsch, Mathematik oder Geschichte
- `[PAKETTITEL]`: kurze, eindeutige Bezeichnung
- `[STUFE/PHASE]`: Zielgruppe, z. B. 8/9/10
- `[KAPITEL]`: fachliche Hauptbereiche
- `[AKZENTFARBE]`: standardmäßig ASW-Rot `#9d1f2f`
- `[LOGO-PFAD]`: lokales Schullogo
- `[LOGO-LINK]`: Website der Schule
- `[SPEICHERSCHLUESSEL]`: eindeutiger, versionsfähiger localStorage-Schlüssel

## Projektstruktur

Verwende nach Möglichkeit diese Struktur:

```text
projekt/
├── index.html                  # vorgeschaltete Paketauswahl/Startseite
├── assets/
│   └── asw-logo.png
├── paket-1/
│   ├── index.html
│   └── assets/
├── paket-2/
│   ├── index.html
│   └── assets/
└── docs/                       # veröffentlichbare GitHub-Pages-Fassung
    └── ...
```

Falls nur ein Lernpaket benötigt wird, darf dessen `index.html` direkt im Projektstamm liegen. Alle verwendeten Medien müssen lokal verfügbar sein. Verwende keine CDN-, Tracking-, Analyse- oder Schriftanbieter.

## Gestaltungsprinzipien

Das Erscheinungsbild ist ruhig, schulisch, übersichtlich und hochwertig. Verwende viel Weißraum, weiße Karten, dezente Schatten und eine dunkelrote Leitfarbe. Bunte Kapitelakzente dürfen Inhalte unterscheiden, sollen die rote Hauptgestaltung aber nicht verdrängen.

Nutze zentral definierte CSS-Variablen:

```css
:root {
  --ink: #252525;
  --muted: #666;
  --accent: #9d1f2f;
  --accent-dark: #741622;
  --paper: #fff;
  --line: #d8d8d8;
  --blue: #063970;
  --green: #277a32;
  --orange: #ef7d00;
  --teal: #008491;
  --violet: #6b3fa0;
  --danger: #b3261e;
  --success: #226c3f;
  --radius: 8px;
  --shadow: 0 16px 34px rgba(45, 45, 45, .13);
}
```

Weitere Vorgaben:

- Schrift: `"Segoe UI", Arial, sans-serif`
- Fließtextfarbe: `var(--ink)`
- Sekundärtext: `var(--muted)`
- Karten: weiß, `1px` Rahmen, `8–10px` Radius, dezenter Schatten
- Primärbuttons: roter Hintergrund, weißer Text, gut sichtbarer Hover-/Fokuszustand
- Interaktive Elemente: mindestens etwa `42px` hoch
- Überschriftenhierarchie semantisch korrekt mit `h1`, `h2`, `h3`
- Keine übermäßigen Rundungen, Glaseffekte oder dekorativen Animationen

## Start- und Paketauswahlseite

Die Startseite erhält:

1. einen breiten roten Kopfbereich,
2. eine kurze Kennzeichnung oberhalb der Hauptüberschrift,
3. einen responsiven Titel,
4. das Schullogo oben rechts,
5. pro Lernpaket eine große anklickbare Themenkarte,
6. ein passendes Vorschaubild auf jeder Karte,
7. optional eine Fortschrittsübersicht unterhalb der Paketauswahl.

Das Logo muss vollständig anklickbar sein:

```html
<a href="[LOGO-LINK]" target="_blank" rel="noopener noreferrer"
   aria-label="Website der Schule öffnen">
  <img class="site-logo" src="[LOGO-PFAD]" alt="Logo der Schule">
</a>
```

Auf größeren Bildschirmen stehen Paketkarten nebeneinander. Unter ungefähr `680px` werden sie einspaltig dargestellt. Vorschaubilder dürfen auf kleinen Displays oberhalb des Kartentextes erscheinen.

## Aufbau einer Lernpaketseite

Die Desktopansicht besteht aus einer festen beziehungsweise dauerhaft sichtbaren Seitennavigation links und dem Hauptbereich rechts.

### Seitennavigation

Die Navigation enthält:

- kompakte Paket-/Fachbezeichnung,
- Gesamtfortschrittsanzeige,
- nach Kapiteln gruppierte Themen,
- aktiven Zustand mit roter Hervorhebung,
- sichtbare Erledigt-Markierung,
- Schaltfläche zum Zurücksetzen des Fortschritts.

Jedes Navigationselement muss ein echtes `button`-Element sein. Aktive und abgeschlossene Zustände dürfen nicht ausschließlich über Farbe vermittelt werden.

### Rote Titelleiste

Der Hauptbereich beginnt mit einer sticky Titelleiste in `var(--accent)`. Sie enthält:

- links Kapitel oder aktuellen Themenpfad,
- eine helle Titelplakette mit `[FACH] [PAKETTITEL] [STUFE/PHASE]`,
- darunter oder daneben lokale Logos/Icons,
- Schaltflächen wie „Überblick“ und „Thema verstanden“.

Lange Titel müssen umbrechen können und dürfen weder Logo noch Bedienelemente überdecken.

### Inhaltsbereich

Strukturiere jedes Thema möglichst in dieser Reihenfolge:

1. kurze Orientierung oder Lernziel,
2. Übersichtsgrafik bzw. visueller Einstieg,
3. verständliche Erklärung mit Beispielen,
4. interaktive Übungsaufgaben,
5. unmittelbares, konkretes Feedback,
6. optionale Vertiefungsaufgabe,
7. Markierung als verstanden/abgeschlossen.

Verwende Karten und Panels, um Sinnabschnitte zu trennen. Lange Textwände sind zu vermeiden. Fachliche Farbcodes müssen innerhalb eines Pakets konsistent bleiben.

## Aufgaben und Rückmeldungen

Jede Aufgabe muss ohne Vorwissen über die Bedienlogik eindeutig erklären:

- was verändert, gewählt, zugeordnet oder eingetragen werden soll,
- wie viele Eingaben erwartet werden,
- welche Zielstruktur oder Zeitform gesucht ist,
- wann die Eingabe geprüft wird.

Wenn eine Lösung aus getrennten Satzbestandteilen besteht, verwende mehrere Eingabefelder oder Dropdown-Menüs an den grammatisch passenden Positionen. Erzeuge niemals durch ein einziges Dropdown einen syntaktisch falschen Satz.

Rückmeldungen sollen konkret sein:

- richtig: kurze Bestätigung und gegebenenfalls Begründung,
- falsch: hilfreicher Hinweis auf die relevante Regel,
- keine Eingabe: Aufforderung, die fehlenden Felder zu bearbeiten.

Die Lösung darf nicht allein durch rote/grüne Farbe erkennbar sein. Ergänze Text, Symbol oder Statuskennzeichnung und nutze für dynamisches Feedback `aria-live="polite"`.

## Fortschritt und Statistik

Speichere den Fortschritt zentral über eine klar abgegrenzte JavaScript-Schicht. Die Oberfläche soll nicht direkt an vielen Stellen auf `localStorage` zugreifen.

Ein sinnvoller Datensatz enthält:

```js
{
  schemaVersion: 1,
  updatedAt: "ISO-DATUM",
  packages: {
    "paket-id": {
      exercises: {
        "thema-id": { attempted: 0, correct: 0 }
      },
      finalTest: {
        attempted: false,
        correct: 0,
        total: 0,
        sections: {}
      }
    }
  }
}
```

Regeln:

- Versionsfähigen, projektspezifischen Speicherschlüssel verwenden.
- Fehlerhafte oder veraltete Daten defensiv behandeln.
- Fortschritt beim Prüfen einer Aufgabe aktualisieren, nicht schon beim bloßen Öffnen.
- Mehrfaches Klicken darf Zähler nicht unkontrolliert erhöhen.
- Zurücksetzen nur nach klarer Bestätigung.
- Export als lesbare JSON-Datei anbieten.
- Importdatei validieren und vor Überschreiben nachfragen.
- Keine Namen oder sonstigen personenbezogenen Daten im Browser speichern.

Wenn eine Statistik vorhanden ist, gilt:

- äußerer Ring: Ergebnis des Abschlusstests,
- innerer Ring: Anteil korrekter Lösungen an den bearbeiteten Übungen,
- `100 %` entspricht einem vollständig gefüllten Ring,
- Prozentwerte zusätzlich als Text ausgeben,
- bei noch fehlenden Daten „Noch nicht bearbeitet“ anzeigen.

Die Speicherlogik soll später durch einen SCORM-, LTI- oder API-Adapter ergänzt werden können, ohne die gesamte Benutzeroberfläche umzubauen.

## Responsive Verhalten

Die Anwendung muss mindestens bei Desktop, Tablet und Smartphone funktionieren.

- Unter etwa `1040px`: mehrspaltige Inhaltsbereiche reduzieren.
- Unter etwa `680px`: Seitennavigation und Inhalt untereinander; Titelleiste vertikal; reduzierte Außenabstände.
- Keine horizontal abgeschnittenen Aufgaben, Tabellen oder Dropdowns.
- Bilder mit `max-width: 100%` und sinnvoller Höhenbegrenzung darstellen.
- Sticky Elemente auf kleinen Displays nur beibehalten, wenn sie keinen wesentlichen Inhalt verdecken.
- Mit `@media (prefers-reduced-motion: reduce)` nicht notwendige Bewegungen deaktivieren.

## Barrierefreiheit

- Dokumentensprache über `<html lang="de">` setzen.
- Jede Seite besitzt genau ein aussagekräftiges `h1`.
- Alle Bilder erhalten passende `alt`-Texte; rein dekorative Bilder `alt=""`.
- Alle Funktionen müssen per Tastatur erreichbar sein.
- Sichtbare Fokuszustände niemals ersatzlos entfernen.
- Formularelemente benötigen sichtbare Beschriftungen oder eindeutige `aria-label`-Attribute.
- Ausreichende Farbkontraste einhalten.
- Dynamische Statusmeldungen über Live-Regionen zugänglich machen.
- Links, Buttons und Navigation semantisch korrekt einsetzen.

## Medien und Dateigröße

- Bilder bevorzugt als WebP verwenden.
- Logos mit Transparenz dürfen PNG bleiben.
- Keine unnötig hochauflösenden oder doppelt vorhandenen Dateien ausliefern.
- Das veröffentlichbare Verzeichnis `docs/` darf insgesamt höchstens `25 MB` groß sein.
- Keine externen Medien einbinden, wenn sie lokal bereitgestellt werden können.
- Pfade relativ halten, damit lokale Nutzung und GitHub Pages gleichermaßen funktionieren.

## Technische Regeln

- Bevorzuge eine einzelne, eigenständige `index.html` pro Paket mit internem CSS und JavaScript.
- Verwende valides HTML5 und moderne, breit unterstützte Browser-APIs.
- Keine Frameworks, Paketmanager oder Build-Schritte ohne ausdrückliche Anforderung.
- Keine Geheimnisse, Tokens oder API-Schlüssel in HTML/JavaScript hinterlegen.
- Nutzerinhalte sicher als Text einsetzen; nicht ungeprüft über `innerHTML` ausgeben.
- Bestehende Nutzeränderungen und fachliche Inhalte nicht ungefragt überschreiben.
- Bei paralleler Pflege von Arbeits- und `docs`-Fassung müssen die ausgelieferten Dateien inhaltlich identisch bleiben.

## Prüfung vor Übergabe

Führe mindestens diese Kontrollen durch:

1. Alle lokalen Links und Medienpfade existieren.
2. Jede Inline-JavaScript-Sektion lässt sich ohne Syntaxfehler parsen.
3. Es gibt keine doppelten HTML-IDs.
4. Navigation, Aufgabenprüfung, Reset, Export und Import funktionieren.
5. Fortschritt bleibt nach Neuladen erhalten.
6. Layout funktioniert bei ungefähr `1440px`, `1024px`, `768px` und `375px` Breite.
7. Tastaturnavigation und sichtbarer Fokus funktionieren.
8. Arbeits- und `docs`-Fassung stimmen überein.
9. `docs/` bleibt unter `25 MB`.
10. Die Seite funktioniert über einen lokalen HTTP-Server und verwendet keine absoluten lokale Dateipfade.

## Abnahmekriterien

Das Ergebnis ist fertig, wenn es visuell zum bestehenden ASW-Lernpaketstil passt, fachlich verständlich, responsiv und tastaturbedienbar ist, den Fortschritt zuverlässig speichert und ohne Installation als statische Website ausgeliefert werden kann.
