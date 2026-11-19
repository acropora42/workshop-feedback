# Workshop-Feedback — Live-Demo für agentisches Coding

## Worum es geht

Dieses Projekt ist eine **Live-Demo in einem KI-Workshop**. Das Publikum sind
10–15 Führungskräfte der österreichischen Volkshochschulen, also keine
Techniker:innen. Vor ihren Augen entsteht in etwa 20–30 Minuten eine kleine App:

- Die Teilnehmenden scannen einen **QR-Code** und geben am Handy Feedback zum
  Workshop (Start: 1–5 Sterne und ein kurzer Kommentar).
- Eine **Beamer-Ansicht** zeigt die Auswertung live, neue Antworten erscheinen
  ohne Neuladen.
- Danach wird die App nach **Wünschen aus dem Publikum** erweitert
  (z. B. zusätzliche Fragen, Filter, Export).

Die Botschaft: Man beschreibt in normaler Sprache, was man will, und die KI
setzt es um, auch Datenbank und Online-Stellen. SQL oder Code muss niemand
selbst schreiben oder hineinkopieren.

## Wie du in dieser Demo kommunizierst

- **Deutsch**, einfache Sprache, Fachbegriffe kurz erklären.
- Vor jedem größeren Schritt in **einem Satz** sagen, was du tust und warum, so
  dass es ein Management-Publikum am Beamer mitverfolgen kann.
- Im Chat keine langen Code-Blöcke zeigen. Code gehört in die Dateien.
- Bilder, die gut ankommen: „Die App ist der Fragebogen, die Datenbank ist die
  Urne, der Beamer zählt live aus.“

## Technik

- **Eine einzige Datei `index.html`** (HTML, CSS, JavaScript). Kein Build-Schritt,
  kein Framework, kein npm. Supabase-JS über CDN mit fester Versionsnummer.
- Handy-Ansicht und Beamer-Ansicht in derselben Datei, z. B. über `?beamer`
  in der Adresse.
- Die Handy-Ansicht ist **mobil zuerst** gestaltet: große Tasten, wenig Text.
  Die Beamer-Ansicht hat große Schrift und hohen Kontrast und zeigt den QR-Code
  zur Handy-Ansicht gleich mit an.
- **Datenbank: Supabase**, Projekt `cpsjjfbtazjyxpkmeljl`, Region Frankfurt (EU).
  - Claude ist über den **Supabase-MCP-Server** angebunden (nur dieses Projekt)
    und legt Tabellen, Zugriffsregeln und Realtime selbst an.
  - Zugriffsregeln (RLS): anonyme Nutzer dürfen **nur einfügen und lesen**,
    nicht ändern oder löschen. Eingaben in der Datenbank begrenzen
    (Wertebereiche, Textlänge).
  - In der App steht nur der **Publishable/anon key**. Der ist öffentlich
    gedacht und durch RLS abgesichert. **Niemals** den Secret- bzw.
    service_role-Key verwenden oder in Dateien schreiben.
  - Für die Live-Auswertung Supabase Realtime nutzen.
- **Hosting: GitHub Pages** aus einem **öffentlichen** GitHub-Repo (GitHub Free).
  Im Repo stehen keine Geheimnisse.

## Regeln

- **Keine echten Personendaten.** Feedback ist anonym, es gibt keine Namen und
  keine E-Mail-Adressen. (DSGVO-Frage kommt sicher, Daten liegen in Frankfurt.)
- **Vor jedem `git push` fragen.** Der Push macht die Seite öffentlich.
- Kleine, sinnvolle Commits als **Rücksprungpunkte**, falls live etwas hakt.

## Stand (19.11.2026)

- [x] Supabase-Konto und Projekt angelegt
- [x] Supabase-MCP für diesen Ordner eingerichtet (Freigabe per `/mcp` → Authenticate)
- [x] Verbindung testen: „Welche Tabellen gibt es?“ (erwartet: keine) — erfolgreich, keine Tabellen
- [x] GitHub-Repo anlegen und GitHub Pages einschalten
      → Repo: https://github.com/acropora42/workshop-feedback (öffentlich)
      → Seite: https://acropora42.github.io/workshop-feedback/ (aus `main`, Wurzel)
- [ ] Probelauf: App komplett bauen, mit 2–3 Handys testen
- [ ] Zurücksetzen auf den Stand vor der App (Tabelle wieder löschen) als
      Startpunkt für den Workshop
- [x] Entscheiden: Live-Demo in VS Code oder in der Claude-Desktop-App
      → **Claude-Desktop-App (Bereich „Code“)**, VS Code bleibt als Ersatz.
      Probelauf findet in der Desktop-App statt.
