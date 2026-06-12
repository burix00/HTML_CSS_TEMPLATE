# HTML Referenz & Tipps: Vom Papier-Mockup zur Website

Diese Referenz hilft dir dabei, eine physische Skizze (Papier-Mockup) strukturiert in funktionierenden HTML-Code umzuwandeln.

## 1. Der Workflow: Vom Papier zum Code

Der wichtigste Schritt passiert **bevor** du Code schreibst – direkt auf dem Papier:
1. **Boxen einzeichnen:** Nimm dir einen Stift und zeichne Rechtecke um alle logischen Bereiche deines Papier-Mockups.
2. **Von außen nach innen (Top-Down):** Fang bei der größten Box an (z.B. der ganzen Seite oder dem `<body>`), dann der Hauptbereich, dann ein Raster darin, dann die einzelnen Elemente darin.
3. **Gemeinsame Container identifizieren:** Überlege dir, welche Elemente nebeneinander stehen sollen. Diese brauchen IMMER einen gemeinsamen Container (z.B. ein `<div>`, `<section>` oder `<nav>`), den du später mit CSS (Flexbox oder Grid) anordnen kannst. Ohne Eltern-Container ist ein Nebeneinander-Anordnen sehr schwer!
4. **Klassen vergeben:** Überlege dir schon auf dem Papier sinnvolle, englische Klassennamen für die Boxen (z.B. `.hero-section`, `.card-grid`, `.sidebar`).

## 2. Das HTML5 Grundgerüst

Jede HTML-Datei startet mit diesem Gerüst:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Titel der Webseite</title>
    <link rel="stylesheet" href="style.css"> <!-- WICHTIG: CSS Verlinkung -->
</head>
<body>
    <!-- Hier kommt der sichtbare Inhalt hin -->
</body>
</html>
```

## 3. Semantisches HTML (Die richtigen Container wählen)

Verwende nicht immer nur `<div>`-Tags (die sogenannte "Div-Suppe"). Nutze semantische Container. Sie helfen dabei, die Seite logisch zu gliedern:

*   `<header>`: Der oberste Kopfbereich deiner Seite (enthält oft das Logo und die Navigation).
*   `<nav>`: Bereich für Haupt- oder Untermenüs (meistens mit einer ungeordneten Liste `<ul>` im Inneren).
*   `<main>`: Der Hauptinhalt der Seite. Darf nur einmal pro Seite vorkommen.
*   `<section>`: Ein thematischer Abschnitt im Design (z.B. "Über uns", "Preise", "Features"). Hat fast immer eine eigene Überschrift (`<h2>`).
*   `<article>`: Ein unabhängiger, in sich geschlossener Inhaltsteil (z.B. eine News-Meldung, ein Blogbeitrag, eine Detail-Karte).
*   `<aside>`: Seitenleisten (Sidebar) oder Zusatzinfos.
*   `<footer>`: Der Fußbereich ganz unten (Impressum, Copyright-Links).

*Tipp: Wenn du ein Element hast, dem keine dieser Bedeutungen zugeordnet werden kann (z.B. nur ein Hüll-Element, um zwei Layout-Boxen zu umschließen), dann ist ein `<div>` absolut richtig!*

## 4. Wichtige innere Elemente

*   **Überschriften:** `<h1>` bis `<h6>`. Verwende `<h1>` nur einmal pro Seite! Danach strukturieren wie ein Inhaltsverzeichnis (z. B. auf `<h2>` folgt `<h3>`).
*   **Textabschnitte:** `<p>` (Paragraph) für fließenden Text.
*   **Bilder:** `<img src="bild.jpg" alt="Bildbeschreibung">`. *Das `alt`-Attribut muss immer rein, auch wenn es leer bleibt!*
*   **Links:** `<a href="link-ziel.html">Hier klicken</a>`.
*   **Listen (Sehr wichtig für Menüs!):**
    ```html
    <ul> <!-- ungeordnete Liste -->
        <li>Punkt 1</li>
        <li>Punkt 2</li>
    </ul>
    ```
*   **Buttons:** `<button type="button">Senden</button>`. *Nicht mit `<a href="...">` verwechseln. Links führen zu neuen Seiten, Buttons lösen Aktionen aus.*

## 5. Formulare & Eingabefelder (Forms)

Eingabefelder sind essenziell für die Interaktion (z.B. Kontaktformulare, Login-Bereiche). 

```html
<form action="/submit" method="POST">
    <!-- Label und Input über das for/id Attribut verknüpfen (wichtig für Barrierefreiheit!) -->
    <div class="form-group">
        <label for="username">Name:</label>
        <input type="text" id="username" name="name" placeholder="Max Muster" required>
    </div>
    
    <div class="form-group">
        <label for="email">E-Mail:</label>
        <input type="email" id="email" name="email" required>
    </div>

    <!-- Dropdown-Auswahl -->
    <div class="form-group">
        <label for="topic">Thema:</label>
        <select id="topic" name="topic">
            <option value="support">Support</option>
            <option value="sales">Verkauf</option>
        </select>
    </div>

    <!-- Mehrzeiliges Textfeld -->
    <div class="form-group">
        <label for="msg">Nachricht:</label>
        <textarea id="msg" name="message" rows="5"></textarea>
    </div>

    <!-- Auslöser zum Senden -->
    <button type="submit">Absenden</button>
</form>
```
*Tipp: Gängige Input-Typen sind `text`, `email`, `password`, `number`, `checkbox` und `radio`.*

## 6. Links & Navigation im Detail

Oft reicht ein normaler Link nicht aus. Hier die wichtigsten Varianten:

*   **Neuen Tab öffnen:** `<a href="https://google.com" target="_blank" rel="noopener">Google</a>`
*   **Sprungmarke (Anker-Link):** Zeigt auf eine `id` auf derselben Seite.
    *   Zielanker auf der Seite: `<section id="kontakt">...</section>`
    *   Der Link dorthin: `<a href="#kontakt">Zum Kontakt</a>`
*   **E-Mail-Link:** Öffnet das lokale E-Mail-Programm: `<a href="mailto:info@beispiel.de">Schreib uns</a>`
*   **Telefon-Link:** Wählt am Smartphone direkt die Nummer: `<a href="tel:+49123456789">Anrufen</a>`

## 7. Block- vs. Inline-Elemente (WICHTIG!)

Das Verständnis dieses Konzepts ist extrem wichtig für das spätere CSS-Layout:

*   **Block-Elemente:** Nehmen immer die **volle verfügbare Breite** ein und erzeugen davor und danach einen Zeilenumbruch. (Man kann sie sich als "Kisten" vorstellen, die sich übereinander stapeln).
    *   *Beispiele:* `<div>`, `<p>`, `<h1>` bis `<h6>`, `<section>`, `<ul>`, `<li>`, `<footer>`
*   **Inline-Elemente:** Nehmen nur **genau so viel Breite ein, wie ihr Inhalt benötigt**. Sie verursachen keine umgebenden Zeilenumbrüche, der Text fließt normal neben ihnen weiter.
    *   *Beispiele:* `<span>`, `<a>`, `<strong>`, `<em>`, `<img>` (Bilder sind "inline-block")

## 8. Globale Attribute & Zuweisungen

Bestimmte Attribute können an (fast) *jedes* HTML-Element angehängt werden:

*   `class="..."` : Um Elemente zu gruppieren und später mit CSS / JavaScript anzusprechen (Kann mehrfach vergeben werden: `class="btn btn-primary"`).
*   `id="..."` : Eindeutige Kennung. Darf pro HTML-Seite **nur EINMAL** vorkommen! Gut für Sprungmarken oder wichtiges JavaScript.
*   `title="..."` : Kleiner Tooltip-Text, der beim "Hovern" mit der Maus nach kurzer Zeit erscheint.
*   `style="..."` : Inline-CSS direkt am Element (Sollte man nach Möglichkeit vermeiden, CSS gehört in die `.css`-Datei!).

## 9. Tabellen (Tables)

Nur für **echte tabellarische Daten** verwenden (z.B. Preislisten, Öffnungszeiten, Termine), **niemals für das Seitenlayout!**

```html
<table>
    <thead>
        <tr> <!-- tr = Table Row (Zeile) -->
            <th>Produkt</th> <!-- th = Table Header (Spaltenkopf) -->
            <th>Preis</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Standard Paket</td> <!-- td = Table Data (Zelle) -->
            <td>19,00 €</td>
        </tr>
    </tbody>
</table>
```

## 10. Medien und Embeds

So bindest du externe Medien oder Dokumente barrierefrei ein:

```html
<!-- Video mit integrierten Steuerelementen (Play/Pause/Ton) -->
<video controls width="100%">
    <source src="film.mp4" type="video/mp4">
    Dein Browser kann dieses Video offenbar nicht abspielen.
</video>

<!-- Einbinden (Embed) von z.B. YouTube-Videos oder Google Maps -->
<iframe src="https://www.youtube.com/embed/XXXXXX" width="560" height="315" allowfullscreen></iframe>
```

## 11. Tipps für die Umsetzung / Prüfung (Der Workflow)

1. **HTML zuerst, CSS später:** Baue erst das vollständige HTML-Gerüst auf. Wenn der Text und die Bilder richtig untereinander stehen, hast du eine solide Basis. Erst dann fängst du mit CSS (Farben, Layout) an.
2. **Sauber einrücken (Indentation):** Verschachtelte Elemente MÜSSEN immer eingerückt werden. Das sieht nicht nur schöner aus, sondern hilft dir sofort zu erkennen, wo ein Container beginnt und wo er endet. In VS Code: Rechtsklick -> "Format Document" hilft dabei.
3. **Sichtbare Strukturierung (Kommentare):** Strukturiere deinen Code aktiv mit HTML-Kommentaren, um dich selbst und andere zurechtzufinden: `<!-- Hier beginnt der Header -->`.
4. **Der Dummy-Inhalt:** Wenn dir beim Übersetzen vom Papier Text fehlt, verwende "Lorem Ipsum" oder einfache Platzhalterworte. Gleiches gilt für Platzhalter-Bilder. Schnelle Platzhalter-Bilder gibt es z.B. via: `<img src="https://via.placeholder.com/300x200" alt="Placeholder">`.
5. **Kleine Schritte testen:** Wenn du eine HTML-Struktur gebaut und mit CSS angeordnet hast (z.B. nur die Navbar), speichere und schau es dir direkt im Browser an, bevor du mit dem nächsten Riesenteil weitermachst.