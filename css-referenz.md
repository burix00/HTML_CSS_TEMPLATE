# CSS Prüfungs-Referenz

> **Ziel dieser Datei:** Alle wichtigen CSS-Eigenschaften auf einen Blick – optimiert für die Prüfung, wo ein Mockup rekonstruiert werden muss.

---

## Inhaltsverzeichnis
1. [Selektoren Cheat-Sheet](#1-selektoren-cheat-sheet)
2. [Farben & Hintergrund](#2-farben--hintergrund)
3. [Schrift & Text](#3-schrift--text)
4. [Box-Modell (Größe, Abstände, Rahmen)](#4-box-modell-größe-abstände-rahmen)
5. [Schatten & Effekte](#5-schatten--effekte)
6. [Bilder korrekt einbinden](#6-bilder-korrekt-einbinden)
7. [Buttons & Formulare stylen](#7-buttons--formulare-stylen)
8. [Transitions & Hover-Effekte](#8-transitions--hover-effekte)
9. [Häufige Fehler & Lösungen](#9-häufige-fehler--lösungen)
10. [Vollständige Mockup-Checkliste](#10-vollständige-mockup-checkliste)

---

## 1. Selektoren Cheat-Sheet

```css
/* Grundlegende Selektoren */
div          { }  /* Alle <div> Elemente */
.klasse      { }  /* Alle Elemente mit class="klasse" */
#id          { }  /* Das Element mit id="id" */
*            { }  /* ALLE Elemente */

/* Kombinations-Selektoren */
.parent .child  { }  /* .child das irgendwo IN .parent ist */
.parent > .child{ }  /* DIREKTE Kinder von .parent */
h1 + p          { }  /* <p> direkt nach <h1> */
h2 ~ p          { }  /* Alle <p> nach <h2> auf gleicher Ebene */
div, p, span    { }  /* Mehrere gleichzeitig (Komma = oder) */

/* Attribut-Selektoren */
input[type="text"]    { }  /* Input mit type="text" */
a[href]               { }  /* Links die ein href haben */
a[href^="https"]      { }  /* href beginnt mit "https" */
a[href$=".pdf"]       { }  /* href endet mit ".pdf" */
a[href*="google"]     { }  /* href enthält "google" */

/* Pseudo-Klassen (Zustände) */
a:hover        { }  /* Wenn Maus drüber */
a:active       { }  /* Beim Klicken */
a:visited      { }  /* Schon besucht */
input:focus    { }  /* Hat Fokus (Tab/Klick) */
:nth-child(1)  { }  /* 1. Kind */
:nth-child(odd){ }  /* Ungerade: 1, 3, 5 */
:nth-child(even){ } /* Gerade: 2, 4, 6 */
:first-child   { }  /* Erstes Kind */
:last-child    { }  /* Letztes Kind */
:not(.active)  { }  /* Alles außer .active */

/* Pseudo-Elemente */
::before { content: ""; }  /* Eingefügtes Element davor */
::after  { content: ""; }  /* Eingefügtes Element danach */
::placeholder { }          /* Input Placeholder-Text */
::selection   { }          /* Vom User ausgewählter Text */
```

---

## 2. Farben & Hintergrund

### Farb-Notationen

```css
/* Alle sind äquivalent für Rot: */
color: red;
color: #ff0000;
color: #f00;          /* Kurzform */
color: rgb(255, 0, 0);
color: rgba(255, 0, 0, 0.8);   /* 0.8 = 80% opak */
color: hsl(0, 100%, 50%);
```

### Nützliche Farben

```css
/* Grautöne */
color: #111;    /* Fast schwarz */
color: #333;    /* Dunkelgrau (gut für Text) */
color: #666;    /* Mittelgrau */
color: #999;    /* Hellgrau */
color: #ccc;    /* Sehr hell */
color: #eee;    /* Hintergrund-Grau */
color: #f5f5f5; /* Fast weiß */

/* Transparente Overlays */
background: rgba(0, 0, 0, 0.3);    /* 30% schwarz */
background: rgba(0, 0, 0, 0.5);    /* 50% schwarz (Standard-Overlay) */
background: rgba(255, 255, 255, 0.9); /* Weißes Overlay */
```

### Hintergrund-Kurzformen

```css
/* Nur Farbe */
background: #3498db;

/* Nur Bild */
background: url("bild.jpg") center/cover no-repeat;

/* Farbe + Bild */
background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
            url("hero.jpg") center/cover no-repeat;
/* TRICK: Farbiger Overlay über Hintergrundbild! */
```

### Gradients

```css
/* Links → Rechts */
background: linear-gradient(to right, #3498db, #9b59b6);

/* Diagonal (45 Grad) */
background: linear-gradient(45deg, #ff6b6b, #ffd93d);

/* Mehrere Farben */
background: linear-gradient(to right, red 0%, yellow 50%, green 100%);

/* Kreisförmig */
background: radial-gradient(circle, #fff, #000);
```

### Wichtige background-Eigenschaften

| Property | Häufigste Werte | Wann |
|---|---|---|
| `background-color` | `#3498db`, `transparent` | Hintergrundfarbe |
| `background-image` | `url("...")` | Bild als Hintergrund |
| `background-size` | **`cover`**, `contain`, `100%` | Wie das Bild skaliert |
| `background-position` | **`center`**, `top`, `50% 50%` | Wo das Bild liegt |
| `background-repeat` | **`no-repeat`**, `repeat` | Wiederholen? |
| `background-attachment` | `scroll`, **`fixed`** (Parallax) | Scrollt mit? |

---

## 3. Schrift & Text

### Schrift-Kurzformen

```css
/* font: style weight size/line-height family */
font: normal bold 1.2rem/1.6 Arial, sans-serif;

/* Einzeln (klarer für die Prüfung) */
font-family: Arial, Helvetica, sans-serif;
font-size: 1rem;      /* = 16px bei Standard */
font-weight: bold;    /* oder: 400, 700, 900 */
font-style: italic;
```

### Einheitentabelle

| Einheit | Beschreibung | Beispiel |
|---|---|---|
| `px` | Pixel (absolut) | `16px` |
| `rem` | Relativ zur Root-Schriftgröße | `1rem = 16px` |
| `em` | Relativ zur Elternelement-Schriftgröße | `2em = 2× Eltern` |
| `%` | Prozent (des Elternelements) | `100% = volle Breite` |
| `vw` | Prozent der Fensterbreite | `100vw = volle Breite` |
| `vh` | Prozent der Fensterhöhe | `100vh = volle Höhe` |
| `fr` | Bruchteil (nur in CSS Grid) | `1fr = gleichmäßig` |

### Text-Eigenschaften

```css
/* Ausrichtung */
text-align: left | right | center | justify;

/* Dekoration */
text-decoration: none;           /* Kein Unterstrich (für Links!) */
text-decoration: underline;
text-decoration: line-through;   /* Durchgestrichen */

/* Transformation */
text-transform: uppercase;   /* GROSSBUCHSTABEN */
text-transform: lowercase;   /* kleinbuchstaben */
text-transform: capitalize;  /* Erster Buchstabe Groß */

/* Überlauf */
white-space: nowrap;         /* Kein Umbruch */
overflow: hidden;
text-overflow: ellipsis;     /* "..." am Ende → mit den beiden oben! */

/* Abstände */
letter-spacing: 0.1em;  /* Zeichenabstand */
word-spacing: 0.5em;    /* Wortabstand */
line-height: 1.6;       /* Zeilenabstand (empfohlen: 1.4–1.8) */

/* Einzug */
text-indent: 2em;       /* Erste Zeile einrücken */
```

### Google Fonts einbinden

```html
<!-- Im <head> -->
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
```

```css
body { font-family: 'Roboto', sans-serif; }
h1, h2, h3 { font-family: 'Poppins', sans-serif; }
```

---

## 4. Box-Modell (Größe, Abstände, Rahmen)

### Das Box-Modell im Überblick

```
┌─────────────────────────────────┐
│            MARGIN               │  ← Außenabstand
│   ┌─────────────────────────┐   │
│   │         BORDER          │   │  ← Rahmen
│   │   ┌─────────────────┐   │   │
│   │   │    PADDING      │   │   │  ← Innenabstand
│   │   │  ┌───────────┐  │   │   │
│   │   │  │  CONTENT  │  │   │   │  ← Inhalt
│   │   │  └───────────┘  │   │   │
│   │   └─────────────────┘   │   │
│   └─────────────────────────┘   │
└─────────────────────────────────┘

MIT box-sizing: border-box (Standard-Empfehlung):
  width = content + padding + border  (alles inklusive!)
  
OHNE (Standard-Browser):
  width = NUR content (padding und border werden addiert!)
```

### Abstände (Kurzschreibweise)

```css
/* Reihenfolge: Oben → Rechts → Unten → Links (Uhrzeigersinn!) */
margin: 10px 20px 15px 5px;   /* oben rechts unten links */
margin: 10px 20px;            /* oben/unten  links/rechts */
margin: 20px;                 /* alle 4 gleich */
margin: 0 auto;               /* zentrieren horizontal! */

/* Einzeln */
margin-top: 10px;
margin-right: 20px;
margin-bottom: 10px;
margin-left: 20px;

/* Gleiches für padding */
padding: 20px;
padding: 10px 20px;
padding-top: 10px;
/* usw. */
```

### Rahmen (border)

```css
/* Kurzform: Breite Stil Farbe */
border: 1px solid #ddd;
border: 2px dashed #3498db;
border: 3px dotted red;
border: none;              /* Kein Rahmen (entfernt Standard-Rahmen!) */

/* Einzelne Seiten */
border-top: 2px solid black;
border-bottom: 1px solid #eee;
border-left: 4px solid #3498db;  /* Linke Markierungslinie */

/* Rahmen-Stile */
/* solid = durchgehend, dashed = gestrichelt, dotted = gepunktet */
/* double = doppelt, groove = 3D-Rille, ridge = 3D-Erhöhung */

/* Abgerundete Ecken */
border-radius: 5px;    /* Leicht abgerundet */
border-radius: 10px;   /* Stärker abgerundet */
border-radius: 20px;   /* Stark abgerundet */
border-radius: 50%;    /* Kreis/Oval */
border-radius: 999px;  /* Pill-Form (für Buttons) */

/* Einzelne Ecken */
border-top-left-radius: 10px;
border-top-right-radius: 10px;
border-bottom-right-radius: 0;
border-bottom-left-radius: 0;
/* Nur obere Ecken rund: */
border-radius: 10px 10px 0 0;
```

### Größen

```css
width: 300px;        /* Feste Breite */
width: 50%;          /* Relativ zum Elternelement */
width: 100%;         /* Volle Breite */
width: auto;         /* Browser entscheidet */
max-width: 1200px;   /* Nicht breiter als 1200px */
min-width: 200px;    /* Nicht schmaler als 200px */

height: 200px;
height: auto;        /* Höhe passt sich Inhalt an */
height: 100%;        /* Volle Höhe des Elternelements */
min-height: 100vh;   /* Mindestens volle Bildschirmhöhe */
```

---

## 5. Schatten & Effekte

### box-shadow

```css
/* box-shadow: x y blur farbe */
box-shadow: 2px 2px 5px rgba(0,0,0,0.2);    /* Einfach */
box-shadow: 0 4px 15px rgba(0,0,0,0.15);    /* Weich von unten */
box-shadow: 0 0 20px rgba(52,152,219,0.5);  /* Glühen */
box-shadow: inset 0 2px 5px rgba(0,0,0,0.2); /* Innenschatten */
box-shadow: none;                            /* Kein Schatten */

/* Schöne Schatten nach Größe */
/* Klein: */  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
/* Mittel: */ box-shadow: 0 4px 12px rgba(0,0,0,0.15);
/* Groß: */   box-shadow: 0 10px 30px rgba(0,0,0,0.2);
/* Beim Hover größer: */
.karte:hover { box-shadow: 0 15px 40px rgba(0,0,0,0.25); }
```

### text-shadow

```css
/* text-shadow: x y blur farbe */
text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
text-shadow: 0 0 10px rgba(255,255,255,0.8);  /* Leuchten */
text-shadow: 2px 2px 0 black;                  /* Kontur */
```

### filter

```css
filter: blur(4px);          /* Unscharf */
filter: brightness(0.7);    /* Dunkler */
filter: brightness(1.3);    /* Heller */
filter: grayscale(100%);    /* Schwarz-Weiß */
filter: sepia(80%);         /* Altes Foto */

/* Für Bilder bei Hover: */
img { filter: grayscale(100%); transition: filter 0.3s; }
img:hover { filter: grayscale(0%); }
```

### opacity

```css
opacity: 0;    /* Unsichtbar (aber Platz bleibt!) */
opacity: 0.5;  /* Halb transparent */
opacity: 1;    /* Voll sichtbar */

/* vs rgba(): opacity macht ALLES transparent inkl. Text */
/* rgba() macht NUR Hintergrundfarbe transparent */
background: rgba(0,0,0,0.5);  /* Nur Hintergrund transparent */
opacity: 0.5;                  /* Alles transparent */
```

---

## 6. Bilder korrekt einbinden

### Responsives Bild (Standard)

```css
img {
  max-width: 100%;   /* Nie breiter als Container */
  height: auto;      /* Seitenverhältnis beibehalten */
  display: block;    /* Entfernt Lücke unter Bild */
}
```

### Bild in festen Container einpassen

```css
.bild-container {
  width: 300px;
  height: 200px;
  overflow: hidden;
}

.bild-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;   /* Füllt Container, schneidet ab */
  object-fit: contain; /* Ganzes Bild sichtbar, Lücken möglich */
}
```

### Kreisförmiges Profilbild

```css
.profilbild {
  width: 100px;
  height: 100px;
  border-radius: 50%;   /* Kreis! */
  object-fit: cover;
}
```

### Hintergrundbild (Hero-Bild)

```css
.hero {
  background-image: url("hero.jpg");
  background-size: cover;          /* Füllt ganzen Bereich */
  background-position: center;     /* Zentriert */
  background-repeat: no-repeat;
  height: 500px;
  
  /* Kurzform: */
  background: url("hero.jpg") center/cover no-repeat;
}
```

---

## 7. Buttons & Formulare stylen

### Standard-Button

```css
.btn {
  display: inline-block;
  padding: 12px 28px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;        /* Hand-Cursor */
  text-decoration: none;  /* Für <a> als Button */
  transition: all 0.2s ease;
}

.btn:hover {
  background-color: #2980b9;
  transform: translateY(-2px);   /* Leichter Hoch-Effekt */
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
}

.btn:active {
  transform: translateY(0);     /* Runter beim Klick */
}
```

### Button-Varianten

```css
/* Outline-Button */
.btn-outline {
  background: transparent;
  border: 2px solid #3498db;
  color: #3498db;
}
.btn-outline:hover {
  background: #3498db;
  color: white;
}

/* Großer Button */
.btn-lg { padding: 16px 40px; font-size: 1.2rem; }

/* Kleiner Button */
.btn-sm { padding: 6px 14px; font-size: 0.875rem; }

/* Runder Button */
.btn-pill { border-radius: 999px; }

/* Volle Breite */
.btn-block { display: block; width: 100%; text-align: center; }
```

### Formularfelder stylen

```css
input[type="text"],
input[type="email"],
input[type="password"],
input[type="number"],
select,
textarea {
  width: 100%;
  padding: 10px 14px;
  font-size: 1rem;
  border: 1px solid #ddd;
  border-radius: 5px;
  background: white;
  color: #333;
  outline: none;
  transition: border-color 0.2s, box-shadow 0.2s;
  box-sizing: border-box;
}

/* Fokus-State */
input:focus,
select:focus,
textarea:focus {
  border-color: #3498db;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
}

/* Fehler-State */
input.error {
  border-color: #e74c3c;
}

/* Placeholder */
::placeholder {
  color: #aaa;
  font-style: italic;
}

/* Label */
label {
  display: block;        /* Eigene Zeile */
  margin-bottom: 6px;
  font-weight: 600;
  color: #333;
}
```

---

## 8. Transitions & Hover-Effekte

### Grundprinzip

```css
/* 1. Basis-State (was animiert werden soll) */
.element {
  background: #3498db;
  transform: scale(1);
  transition: all 0.3s ease;  /* ← IMMER beim Basis-State! */
  /* transition: was  dauer  timing */
}

/* 2. Hover-State (Zielzustand) */
.element:hover {
  background: #2980b9;
  transform: scale(1.05);
}
```

### Timing-Funktionen

| Funktion | Effekt |
|---|---|
| `ease` | Langsam → schnell → langsam (natürlich) |
| `linear` | Gleichmäßig |
| `ease-in` | Langsam anfangen |
| `ease-out` | Langsam aufhören |
| `ease-in-out` | Beides |

### Häufige Hover-Effekte

```css
/* Hochheben (Karten) */
.karte {
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.karte:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 25px rgba(0,0,0,0.2);
}

/* Farbe wechseln */
.link {
  color: #333;
  transition: color 0.2s;
}
.link:hover { color: #3498db; }

/* Hintergrundfarbe */
.menu-item {
  background: transparent;
  transition: background 0.2s;
}
.menu-item:hover { background: rgba(0,0,0,0.1); }

/* Bild zoomen */
.img-zoom-container {
  overflow: hidden;
}
.img-zoom-container img {
  transition: transform 0.5s ease;
}
.img-zoom-container:hover img {
  transform: scale(1.1);
}

/* Unterstrich-Animation */
.nav-link {
  position: relative;
  text-decoration: none;
}
.nav-link::after {
  content: "";
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0;           /* Beginnt mit 0 */
  height: 2px;
  background: #3498db;
  transition: width 0.3s ease;
}
.nav-link:hover::after {
  width: 100%;        /* Wächst auf volle Breite */
}
```

---

## 9. Häufige Fehler & Lösungen

### Problem: Div ist unsichtbar / hat keine Höhe
```css
/* Leere Divs haben keine Höhe! */
.div-ohne-inhalt {
  height: 200px;      /* Explizit setzen */
  min-height: 100px;
}
/* Oder Inhalt hinzufügen (Bilder, Text) */
```

### Problem: margin: auto zentriert nicht
```css
/* Geht NUR mit block-Elementen MIT definierter Breite */
.zentriert {
  width: 800px;       /* ← Breite MUSS gesetzt sein! */
  margin: 0 auto;
}
```

### Problem: position: absolute springt an die falsche Stelle
```css
/* Elternelement MUSS position: relative haben! */
.container {
  position: relative;  /* ← Vergessen = absolute relativ zum <body> */
}
.element {
  position: absolute;
  top: 10px;
  right: 10px;
}
```

### Problem: Elemente überlappen sich obwohl kein position gesetzt
```css
/* Box-Sizing vergessen! */
* { box-sizing: border-box; }  /* ← Immer setzen! */
/* Ohne: width:200px + padding:20px = 240px (zu breit!) */
/* Mit:  width:200px + padding:20px = 200px (korrekt) */
```

### Problem: Bild hat Lücke darunter
```css
img { display: block; }  /* Entfernt Baseline-Lücke */
```

### Problem: z-index funktioniert nicht
```css
/* z-index funktioniert NUR bei positionierten Elementen! */
.element {
  position: relative;  /* ← PFLICHT für z-index */
  z-index: 10;
}
```

### Problem: overflow: hidden schneidet Schatten ab
```css
/* Schatten außerhalb des Elements → overflow:hidden schneidet ab */
/* Schatten zum Elternelement verschieben, nicht zu overflow:hidden Element */
.wrapper { box-shadow: 0 4px 10px rgba(0,0,0,0.2); }
.inner { overflow: hidden; }
```

### Problem: Flexbox-Items haben nicht gleiche Höhe
```css
/* Flexbox streckt automatisch (stretch) */
/* Wenn nicht gewollt: */
.flex-container { align-items: flex-start; }
/* Für gleiche Höhe: align-items: stretch (Standard) */
```

### Problem: 100vh zu hoch auf Mobilgeräten
```css
/* Mobile Browser haben eine Adressleiste */
.fullscreen {
  height: 100vh;
  height: 100dvh;  /* Dynamic Viewport Height - moderner */
}
```

---

## 10. Vollständige Mockup-Checkliste

Wenn du ein Mockup siehst, gehe diese Liste durch:

### 1. HTML-Struktur aufbauen
- [ ] `<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`
- [ ] `<meta charset="UTF-8">` und `<meta name="viewport">`
- [ ] `<link rel="stylesheet" href="style.css">`
- [ ] Semantische Struktur: `<header>`, `<nav>`, `<main>`, `<footer>`
- [ ] Alle Inhalte als korrektes HTML eingetragen

### 2. CSS Reset & Grundlagen
- [ ] `* { box-sizing: border-box; margin: 0; padding: 0; }`
- [ ] `body` Schriftart, Textfarbe, Hintergrundfarbe
- [ ] Bildschirmbreite nutzen: `min-height: 100vh`

### 3. Layout
- [ ] Wie sind die großen Bereiche aufgeteilt? (header, main, footer)
- [ ] Benötigt es Flexbox oder Grid?
- [ ] Sind Elemente zentriert? (`margin: 0 auto` oder `display: flex; justify-content: center`)
- [ ] Abstände zwischen Bereichen (`gap`, `margin`, `padding`)

### 4. Typografie
- [ ] Schriftart gesetzt? (`font-family`)
- [ ] Schriftgrößen korrekt? (`font-size`)
- [ ] Schriftgewichte? (`font-weight`)
- [ ] Textausrichtung? (`text-align`)
- [ ] Farben der Texte?

### 5. Farben & Hintergründe
- [ ] Hintergrundfarben aller Bereiche
- [ ] Hintergrundbilder mit `background-size: cover`
- [ ] Overlays mit `rgba()`

### 6. Abstände & Rahmen
- [ ] Innenabstände (`padding`) für Bereiche
- [ ] Außenabstände (`margin`) zwischen Elementen
- [ ] Rahmen (`border`) wo nötig
- [ ] Abgerundete Ecken (`border-radius`)

### 7. Bilder
- [ ] `max-width: 100%` für responsive Bilder
- [ ] `object-fit: cover` für Bilder in festen Containern
- [ ] `border-radius: 50%` für Profilbilder

### 8. Details & Polish
- [ ] Hover-Effekte auf Links und Buttons
- [ ] `cursor: pointer` auf klickbaren Elementen
- [ ] `text-decoration: none` auf Links
- [ ] Schatten (`box-shadow`) für Tiefenwirkung
- [ ] Transitions für sanfte Übergänge

### 9. Häufige Maße für die Prüfung

```css
/* Container-Breiten */
max-width: 960px;   /* Schmal */
max-width: 1200px;  /* Standard */
max-width: 1400px;  /* Breit */

/* Navbar-Höhe */
height: 60px;
height: 70px;
height: 80px;

/* Hero-Höhe */
min-height: 400px;
min-height: 500px;
height: 100vh;       /* Volle Bildschirmhöhe */

/* Karten-Breite */
width: 300px;
flex: 1 1 280px;
grid-template-columns: repeat(3, 1fr);

/* Standard-Padding */
padding: 20px;       /* Kompakt */
padding: 40px;       /* Normal */
padding: 60px;       /* Großzügig */
padding: 80px 40px;  /* Sektionen */

/* Typographie */
font-size: 0.875rem; /* 14px – Klein */
font-size: 1rem;     /* 16px – Normal */
font-size: 1.25rem;  /* 20px – Groß */
font-size: 1.5rem;   /* 24px – h3 */
font-size: 2rem;     /* 32px – h2 */
font-size: 2.5rem;   /* 40px – h1 */
font-size: 3rem;     /* 48px – Hero-Titel */
```

---

## Schnell-Referenz: Häufigste CSS-Zeilen

```css
/* Die 30 wichtigsten CSS-Zeilen für die Prüfung */

* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: Arial, sans-serif; }

/* Zentrieren */
.container { max-width: 1200px; margin: 0 auto; padding: 0 20px; }
.flex-center { display: flex; justify-content: center; align-items: center; }

/* Layout */
.flex { display: flex; }
.flex-wrap { display: flex; flex-wrap: wrap; gap: 20px; }
.grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
.sidebar-layout { display: grid; grid-template-columns: 250px 1fr; gap: 30px; }

/* Abstände */
.section { padding: 60px 40px; }
.gap-sm { gap: 10px; }
.gap-md { gap: 20px; }
.gap-lg { gap: 40px; }

/* Bilder */
img { max-width: 100%; height: auto; display: block; }
.img-cover { width: 100%; height: 100%; object-fit: cover; }
.circle { border-radius: 50%; }

/* Buttons */
.btn { padding: 12px 28px; border: none; border-radius: 6px; cursor: pointer; }
a { text-decoration: none; color: inherit; }

/* Effekte */
.card { border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); }
.overlay { background: rgba(0,0,0,0.5); }
.transition { transition: all 0.3s ease; }

/* Position */
.relative { position: relative; }
.absolute-fill { position: absolute; top: 0; left: 0; width: 100%; height: 100%; }
.sticky-top { position: sticky; top: 0; z-index: 100; }
.fixed-bottom { position: fixed; bottom: 0; left: 0; width: 100%; }

/* Text */
.text-center { text-align: center; }
.bold { font-weight: bold; }
.uppercase { text-transform: uppercase; }
.truncate { white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
```
