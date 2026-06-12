# Layout & Raster Guide – Elemente positionieren

> **Ziel dieser Datei:** Du bekommst ein Mockup auf Papier – hier steht wie du Elemente exakt positionieren kannst.

---

## Inhaltsverzeichnis
1. [Wie du ein Mockup analysierst](#1-wie-du-ein-mockup-analysierst)
2. [Flexbox – 1D Layout](#2-flexbox--1d-layout)
3. [CSS Grid – 2D Layout](#3-css-grid--2d-layout)
4. [Position (absolut, relativ, fixiert)](#4-position-absolut-relativ-fixiert)
5. [Häufige Layout-Muster](#5-häufige-layout-muster)
6. [Elemente zentrieren (alle Methoden)](#6-elemente-zentrieren-alle-methoden)
7. [Responsive Design im Überblick](#7-responsive-design-im-überblick)

---

## 1. Wie du ein Mockup analysierst

Wenn du ein Mockup auf Papier bekommst, gehe immer in dieser Reihenfolge vor:

### Schritt 1 – Blöcke erkennen
Zeichne gedanklich **rechteckige Boxen** um alle Bereiche:
```
┌──────────────────────────────────────┐
│              HEADER / NAV            │
├──────────────────────────────────────┤
│                HERO                  │
├──────────────┬───────────────────────┤
│   SIDEBAR    │       MAIN            │
├──────────────┴───────────────────────┤
│              FOOTER                  │
└──────────────────────────────────────┘
```

### Schritt 2 – Fragen stellen
- Liegen Elemente **nebeneinander** → **Flexbox** oder **Grid**
- Liegen Elemente **übereinander** (gestapelt) → **position: absolute** oder **z-index**
- Hat es **Spalten + Zeilen** → **CSS Grid**
- Hat es nur eine **Reihe** (Nav-Links, Karten) → **Flexbox**

### Schritt 3 – HTML-Struktur schreiben
```html
<header>...</header>
<main>
  <aside>...</aside>
  <section>...</section>
</main>
<footer>...</footer>
```

### Schritt 4 – CSS von außen nach innen
Erst das große Layout (header, main, footer), dann die Details.

---

## 2. Flexbox – 1D Layout

**Wann verwenden:** Elemente in **einer Reihe** oder **einer Spalte** anordnen.

### Grundprinzip
```
CONTAINER (display: flex)
├── ITEM 1
├── ITEM 2
└── ITEM 3
```

### Cheat-Sheet: Container-Properties

| Property | Werte | Was es tut |
|---|---|---|
| `display` | `flex` | Flexbox aktivieren |
| `flex-direction` | `row` / `column` | Richtung der Hauptachse |
| `flex-wrap` | `wrap` / `nowrap` | Umbricht in neue Zeile |
| `justify-content` | `flex-start` / `center` / `flex-end` / `space-between` / `space-around` / `space-evenly` | Ausrichtung auf **Hauptachse** |
| `align-items` | `flex-start` / `center` / `flex-end` / `stretch` | Ausrichtung auf **Querachse** |
| `gap` | `20px` | Abstand zwischen Items |

### Cheat-Sheet: Item-Properties

| Property | Werte | Was es tut |
|---|---|---|
| `flex` | `1` / `0 0 200px` / `none` | Wachsen/Schrumpfen/Basis |
| `order` | `-1` / `0` / `1` | Reihenfolge ändern |
| `align-self` | `center` / `flex-end` | Einzelnes Item anders ausrichten |

### Visuelle Achsen

```
flex-direction: row (Standard)
──────────────────────→ justify-content (Hauptachse)
│  [Item 1] [Item 2] [Item 3]
↓
align-items (Querachse)


flex-direction: column
│  [Item 1]
│  [Item 2]       → align-items (Querachse)
↓  [Item 3]
justify-content (Hauptachse)
```

### Häufige Kombinationen

```css
/* Elemente zentrieren (horizontal + vertikal) */
.zentriert {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Navigation nebeneinander */
.nav {
  display: flex;
  gap: 20px;
  align-items: center;
}

/* Logo links, Links rechts */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Karten gleichmäßig verteilen, mit Umbruch */
.karten-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}
.karte {
  flex: 1 1 300px;  /* Mindestens 300px, wächst gleich */
}

/* 3 gleiche Spalten */
.drei-spalten {
  display: flex;
  gap: 20px;
}
.spalte {
  flex: 1;  /* Alle gleich breit */
}

/* Sidebar + Hauptinhalt */
.layout {
  display: flex;
  gap: 20px;
}
.sidebar { flex: 0 0 250px; }  /* Sidebar: feste 250px */
.hauptinhalt { flex: 1; }      /* Rest nimmt verbleibenden Platz */
```

---

## 3. CSS Grid – 2D Layout

**Wann verwenden:** Layout hat **Zeilen UND Spalten** (Raster/Tabellen-ähnliches Layout).

### Grundprinzip
```
CONTAINER (display: grid)
┌──────┬──────┬──────┐
│  1   │  2   │  3   │
├──────┼──────┼──────┤
│  4   │  5   │  6   │
└──────┴──────┴──────┘
```

### Spalten und Zeilen definieren

```css
.container {
  display: grid;
  
  /* 3 gleiche Spalten */
  grid-template-columns: 1fr 1fr 1fr;
  /* Kurzform: */
  grid-template-columns: repeat(3, 1fr);
  
  /* Sidebar (250px) + Hauptinhalt (Rest) */
  grid-template-columns: 250px 1fr;
  
  /* 4 Spalten, mittlere breiter */
  grid-template-columns: 1fr 2fr 2fr 1fr;
  
  /* Responsive: so viele Spalten wie reinpassen (min 200px) */
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  
  /* Abstand zwischen Zellen */
  gap: 20px;
  column-gap: 20px;  /* nur zwischen Spalten */
  row-gap: 10px;     /* nur zwischen Zeilen */
}
```

### Item positionieren

```css
/* WICHTIG: Grid-Linien zählen von 1 (links/oben) */
/*
   1    2    3    4
   |    |    |    |
1──┼────┼────┼────┤
   │ A  │ B  │ C  │
2──┼────┼────┼────┤
   │ D  │ E  │ F  │
3──┴────┴────┴────┘
*/

.item-A {
  grid-column: 1 / 2;  /* Von Linie 1 bis Linie 2 = Spalte 1 */
  grid-row: 1 / 2;
}

/* Über MEHRERE Spalten/Zeilen spannen */
.item-gross {
  grid-column: 1 / 3;   /* Von Spalte 1 bis Spalte 3 (= 2 Spalten breit) */
  grid-column: span 2;   /* Einfacher: nimm 2 Spalten */
  
  grid-row: 1 / 3;       /* 2 Zeilen hoch */
  grid-row: span 2;
}

/* Ganze Zeile füllen */
.volle-breite {
  grid-column: 1 / -1;  /* Von erster bis letzter Linie */
}
```

### Benannte Bereiche (Grid Areas) ← sehr nützlich für Mockups!

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr;
  grid-template-rows: 80px 1fr 60px;
  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
  min-height: 100vh;
}

/* Dann jedem Element seinen Bereich zuweisen */
header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
main    { grid-area: main; }
footer  { grid-area: footer; }
```

Visualisierung:
```
┌─────────────────────────────┐
│           header            │
├──────────┬──────────────────┤
│ sidebar  │      main        │
├──────────┴──────────────────┤
│           footer            │
└─────────────────────────────┘
```

### 12-Spalten-Raster (wie Bootstrap)

```css
.grid-12 {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 20px;
}

/* Klassen für Breiten */
.col-1  { grid-column: span 1; }   /* 1/12 */
.col-2  { grid-column: span 2; }   /* 2/12 */
.col-3  { grid-column: span 3; }   /* 1/4 */
.col-4  { grid-column: span 4; }   /* 1/3 */
.col-6  { grid-column: span 6; }   /* 1/2 */
.col-8  { grid-column: span 8; }   /* 2/3 */
.col-12 { grid-column: span 12; }  /* Volle Breite */
```

```html
<div class="grid-12">
  <div class="col-4">Ein Drittel</div>
  <div class="col-4">Ein Drittel</div>
  <div class="col-4">Ein Drittel</div>
</div>
```

---

## 4. Position (absolut, relativ, fixiert)

**Wann verwenden:** Elemente **übereinander legen**, am Rand positionieren, oder am Bildschirm fixieren.

### Übersicht

| Wert | Bezugspunkt | Im Dokumentenfluss? |
|---|---|---|
| `static` | Normal (Standard) | Ja |
| `relative` | Eigene Ausgangsposition | Ja (reserviert Platz) |
| `absolute` | Nächstes **positioniertes** Elternelement | **Nein** |
| `fixed` | Browserfenster (Viewport) | **Nein** |
| `sticky` | Scrollposition im Viewport | Ja (bis zur Klebestelle) |

### position: relative

```css
/* Element leicht von seiner normalen Position verschieben */
.verschoben {
  position: relative;
  top: 10px;    /* 10px nach unten */
  left: 20px;   /* 20px nach rechts */
}
/* WICHTIG: Der ursprüngliche Platz bleibt reserviert! */
```

### position: absolute ← Häufig für Overlays, Badges, Icons

```css
/* Das Elternelement MUSS position: relative haben! */
.karten-container {
  position: relative;  /* ← PFLICHT als Referenzrahmen */
}

/* Badge in der oberen rechten Ecke */
.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  /* Jetzt relativ zu .karten-container positioniert */
}

/* Komplett über den Container legen */
.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
}

/* Absolut zentrieren */
.absolut-zentriert {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  /* translate(-50%,-50%) korrigiert die Verschiebung */
}
```

### position: fixed

```css
/* Bleibt IMMER an derselben Stelle, auch beim Scrollen */
.navbar-fixed {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  background: white;
}

/* Zurück-nach-oben-Button */
.back-to-top {
  position: fixed;
  bottom: 20px;
  right: 20px;
  z-index: 999;
}
```

### position: sticky

```css
/* Scrollt mit bis zu einem Punkt, dann "klebt" es */
.sticky-header {
  position: sticky;
  top: 0;          /* Klebt wenn es den oberen Rand erreicht */
  z-index: 100;
  background: white;
}

/* Sticky Sidebar die mitscrollt */
.sticky-sidebar {
  position: sticky;
  top: 80px;  /* 80px Abstand von oben (z.B. Navbar-Höhe) */
  align-self: flex-start;  /* Bei Flexbox nötig! */
}
```

### z-index – Stapelreihenfolge

```css
/* Höherer z-index = weiter vorne */
.hintergrund  { z-index: 0; }
.inhalt       { z-index: 1; }
.dropdown     { z-index: 100; }
.navbar       { z-index: 200; }
.modal        { z-index: 1000; }
.tooltip      { z-index: 1500; }

/* z-index funktioniert NUR bei positionierten Elementen! */
/* (position: relative/absolute/fixed/sticky) */
```

---

## 5. Häufige Layout-Muster

### Header mit Logo + Navigation

```
[LOGO]           [Link1] [Link2] [Link3] [Button]
```

```css
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 40px;
  height: 70px;
}

.header-nav {
  display: flex;
  gap: 24px;
  list-style: none;
  align-items: center;
}
```

---

### Hero-Section mit Text zentriert

```
┌────────────────────────────────────────┐
│                                        │
│         Großer Überschrift-Text        │
│         Kleinerer Untertitel           │
│           [Button]                     │
│                                        │
└────────────────────────────────────────┘
```

```css
.hero {
  min-height: 500px;
  background: url("hero.jpg") center/cover;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 40px;
}
```

---

### 3-Spalten Karten-Layout

```
┌──────────┐ ┌──────────┐ ┌──────────┐
│  Karte 1 │ │  Karte 2 │ │  Karte 3 │
└──────────┘ └──────────┘ └──────────┘
```

**Mit Flexbox:**
```css
.karten-bereich {
  display: flex;
  gap: 24px;
  flex-wrap: wrap;
}
.karte {
  flex: 1 1 280px;
}
```

**Mit Grid:**
```css
.karten-bereich {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}
```

---

### Sidebar + Hauptinhalt

```
┌───────────┬────────────────────────┐
│           │                        │
│  Sidebar  │      Hauptinhalt       │
│  (250px)  │      (Rest)            │
│           │                        │
└───────────┴────────────────────────┘
```

**Mit Flexbox:**
```css
.layout {
  display: flex;
  gap: 30px;
}
.sidebar {
  flex: 0 0 250px;  /* Feste 250px, wächst/schrumpft nicht */
}
.hauptinhalt {
  flex: 1;          /* Nimmt den restlichen Platz */
}
```

**Mit Grid:**
```css
.layout {
  display: grid;
  grid-template-columns: 250px 1fr;
  gap: 30px;
}
```

---

### Vollständiges Seiten-Layout

```
┌─────────────────────────────────────┐
│              HEADER                 │
├─────────────────────────────────────┤
│              HERO                   │
├────────────┬────────────────────────┤
│  SIDEBAR   │       CONTENT          │
│            │                        │
├────────────┴────────────────────────┤
│              FOOTER                 │
└─────────────────────────────────────┘
```

```css
body {
  display: grid;
  grid-template-rows: auto auto 1fr auto;
  min-height: 100vh;
}

.layout-main {
  display: grid;
  grid-template-columns: 250px 1fr;
  gap: 30px;
  padding: 30px;
  max-width: 1200px;
  margin: 0 auto;
}
```

---

### Bild-Text nebeneinander (wechselnd)

```
Zeile 1:  [BILD]    [TEXT]
Zeile 2:  [TEXT]    [BILD]
```

```css
.bild-text-reihe {
  display: flex;
  gap: 40px;
  align-items: center;
  margin-bottom: 60px;
}

/* Jede zweite Reihe umkehren */
.bild-text-reihe:nth-child(even) {
  flex-direction: row-reverse;
}

.bild-text-reihe img {
  flex: 0 0 45%;
  width: 45%;
  object-fit: cover;
}

.bild-text-reihe .text {
  flex: 1;
}
```

---

### Footer mit 4 Spalten

```
┌──────────┬──────────┬──────────┬──────────┐
│  Logo +  │  Links   │  Links   │  Kontakt │
│  Über    │          │          │          │
└──────────┴──────────┴──────────┴──────────┘
│              © Copyright 2024              │
```

```css
.footer-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 40px;
  padding: 60px 40px 40px;
}

.footer-bottom {
  grid-column: 1 / -1;  /* Volle Breite */
  text-align: center;
  border-top: 1px solid #eee;
  padding-top: 20px;
}
```

---

## 6. Elemente zentrieren (alle Methoden)

### Horizontal zentrieren

```css
/* Block-Element mit fester Breite */
.div-zentriert {
  width: 800px;
  margin: 0 auto;       /* ← Klassisch! */
}

/* Inline-Element */
.parent { text-align: center; }

/* Mit Flexbox */
.parent {
  display: flex;
  justify-content: center;
}

/* Mit Grid */
.parent {
  display: grid;
  justify-items: center;
}
```

### Vertikal zentrieren

```css
/* Flexbox (EMPFOHLEN) */
.parent {
  display: flex;
  align-items: center;
  height: 400px;  /* Elternelement braucht eine Höhe! */
}

/* Grid */
.parent {
  display: grid;
  align-items: center;
  height: 400px;
}

/* Position Absolute */
.child {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
```

### Horizontal + Vertikal zentrieren (perfekt mittig)

```css
/* Methode 1: Flexbox ← EMPFOHLEN */
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Methode 2: Grid */
.parent {
  display: grid;
  place-items: center;  /* Kurzform für align + justify */
}

/* Methode 3: Position */
.child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Methode 4: Margin Auto mit Flex */
.parent { display: flex; }
.child { margin: auto; }
```

---

## 7. Responsive Design im Überblick

### Breakpoints

```css
/* Mobile First (empfohlen) */
/* Standard: Handy */
.container { width: 100%; padding: 16px; }

/* Tablet */
@media (min-width: 768px) {
  .container { max-width: 960px; margin: 0 auto; }
  .grid { grid-template-columns: repeat(2, 1fr); }
}

/* Desktop */
@media (min-width: 1024px) {
  .container { max-width: 1200px; }
  .grid { grid-template-columns: repeat(3, 1fr); }
}
```

### Flexbox wird automatisch responsive

```css
/* Diese Karten passen sich automatisch an */
.karten {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}
.karte {
  flex: 1 1 280px;  /* Mindest 280px → bei kleinen Screens 1 pro Zeile */
}
```

### Grid wird automatisch responsive

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  /* Passt die Spaltenanzahl automatisch an die Bildschirmbreite an! */
}
```

### Navigation auf Mobile verstecken

```css
.nav-links {
  display: flex;
  gap: 20px;
}

@media (max-width: 768px) {
  .nav-links {
    display: none;  /* Auf Mobil ausblenden */
  }
  .hamburger-menu {
    display: block;  /* Hamburger-Icon zeigen */
  }
}
```

---

## Schnell-Referenz für die Prüfung

| Problem | Lösung |
|---|---|
| Elemente nebeneinander | `display: flex` am Container |
| Alles zentriert | `display: flex; justify-content: center; align-items: center` |
| Gleichmäßige Spalten | `display: grid; grid-template-columns: repeat(N, 1fr)` |
| Sidebar + Inhalt | `grid-template-columns: 250px 1fr` |
| Element über Bild | `position: relative` am Bild, `position: absolute` am Text |
| Navbar fixiert | `position: fixed; top: 0; width: 100%; z-index: 100` |
| Element genau mittig | `position: absolute; top: 50%; left: 50%; transform: translate(-50%,-50%)` |
| Div zentrieren | `margin: 0 auto` (bei fester Breite) |
| Karten responsive | `flex: 1 1 300px` + `flex-wrap: wrap` |
| Hintergrundbild füllt aus | `background-size: cover; background-position: center` |
