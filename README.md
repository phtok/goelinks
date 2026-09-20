# goelinks · Kurzlink-Brücke für tools.goetheanum.ch

Statische GitHub-Pages-Seite, die kurze Adressen der Form

```
tools.goetheanum.ch/s/<tier>
```

auf die volle Ziel-URL (bei Kampagnen samt UTM-Parametern) weiterleitet. Die
Auflösung macht die Supabase-Function `go` gegen die Register
`sommer2026_links` (UTM-Generator) und `qr_links` (QR-Generator) — die
Datenbank ist die **einzige Quelle der Wahrheit**. Dieses Repo hält bewusst
keine Link-Liste; neue Kurzlinks entstehen in den Generatoren und wirken sofort.

**Die Brücke ist neutral.** Sie nennt weder Aktion noch Ziel — ein Kurzlink
kann zu allem führen (Tagung, Kampagne, Dokument), und die Zwischenseite darf
nichts davon verraten. Beschluss 20. September 2026, Auslöser: der QR-Link
`ac27` für die Landwirtschaftliche Tagung zeigte kurz ‹weiter zur
Aktionsseite› der Sommeraktion.

## Wie ein neuer Kurzlink entsteht

Nicht hier im Repo, sondern im **UTM-Generator**:
`werkzeuge.goetheanum.ch/apps/utm-generator/` → Ziel-URL + UTM-Merkmale
eintragen, Kurznamen wählen, ins Register schreiben. Der Kurzname wird zum
Pfad `/s/<kurzname>`.

**Slug-Stil:** kurz, klein, ein zweisilbiger Tiername mit Bild (`otter`,
`biber`, `reiher` …). Menschlich abtippbar aus Bio, Caption oder Papier.

## Wie die Weiterleitung läuft

1. Aufruf `tools.goetheanum.ch/s/otter` → GitHub Pages hat keine solche Datei
   und liefert `404.html` aus.
2. Ein kleines Skript in `404.html` liest den letzten Pfadteil (`otter`) und
   ruft `…/functions/v1/go/otter` auf.
3. Die `go`-Function schlägt `otter` in den Registern nach und antwortet
   mit `302` auf die volle Ziel-URL. Unbekannte Kurznamen landen auf
   `goetheanum.ch`.

## Inhalt

- `index.html` — Startseite (verweist auf Generator und Cockpit).
- `404.html` — die Weiterleitungs-Brücke.
- `CNAME` — `tools.goetheanum.ch` (von GitHub Pages gesetzt).

## Gestalt

Bindet Tokens und Basis des Goetheanum-Design-Systems absolut von
`werkzeuge.goetheanum.ch/design-system/` ein — keine eigenen Farb-, Schnitt-
oder Abstandswerte. Hausregeln: siehe `CLAUDE.md` in
[`phtok/goeloggen`](https://github.com/phtok/goeloggen).
