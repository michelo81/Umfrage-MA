# Umfrage: Ethik als Investitionskriterium?

Eigenständige, öffentliche Umfrage-Seite (ohne Login) für die Masterarbeit
"Ethik als Investitionskriterium? Der Einfluss von ESG-Kriterien
(Environment, Social, Governance) auf Investitionsentscheidungen". Läuft in
einem eigenen, von den übrigen Projekten komplett getrennten
Firebase-Projekt (`masterarbeit-umfrage`) — keine Verbindung zu
Familiendaten oder anderen Projekten.

## Schritt 1 — Firestore-Regeln einspielen

1. Auf [console.firebase.google.com](https://console.firebase.google.com)
   das Projekt `masterarbeit-umfrage` öffnen.
2. Links im Menü "Build" → "Firestore Database" → Tab "Regeln".
3. Den kompletten Inhalt von [`firestore.rules`](./firestore.rules) aus
   diesem Ordner einfügen und auf "Veröffentlichen" klicken.

## Schritt 2 — Auf GitHub + Vercel veröffentlichen

1. Neues, eigenes GitHub-Repository anlegen (z.B. `masterarbeit-umfrage`)
   und den Inhalt dieses Ordners hochladen.
2. Auf [vercel.com](https://vercel.com) → "Add New..." → "Project" → das
   Repository importieren → "Deploy" (kein Build-Schritt nötig, reine
   statische Seite).
3. Die Umfrage ist danach unter der `*.vercel.app`-Adresse live — diesen
   Link kannst du direkt an die Zielgruppe verschicken.

## Wie die Daten fließen

- Teilnehmende öffnen den Link, beantworten die Filterfrage und bei "Ja"
  die neun inhaltlichen Fragen.
- Bei "Nein" wird nichts gespeichert — die Umfrage endet sofort mit einem
  Dankeshinweis (siehe `firestore.rules`-Kommentar und die Regel selbst,
  die ausschließlich die neun inhaltlichen Felder zulässt).
- Beim Absenden wird ein neuer, anonymer Eintrag in der Firestore-Sammlung
  `antworten` angelegt — ganz ohne Login, aber streng auf die erlaubten
  Felder/Antwortmöglichkeiten geprüft (siehe `firestore.rules`). Es werden
  keinerlei persönliche Daten erfasst.
- Die Auswertung erfolgt in einer eigenen Ansicht im Familien-Dashboard
  (Menüpunkt "Umfrage"), die sich dafür separat und nur lesend mit diesem
  Firebase-Projekt verbindet.
