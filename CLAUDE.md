# Hausordnung für dieses Projekt

## Worum es geht

Dieses Projekt ist eine **Live-Demo in einem KI-Workshop**. Das Publikum sind
10–15 Führungskräfte der österreichischen Volkshochschulen, also keine
Techniker:innen. Vor ihren Augen entsteht in etwa 20–30 Minuten eine kleine
Web-App. Was die App können soll, sagt der Vortragende live.

Die Botschaft: Man beschreibt in normaler Sprache, was man will, und die KI
setzt es um, auch Datenbank und Veröffentlichung im Internet. SQL oder Code muss
niemand selbst schreiben oder hineinkopieren.

## Erst fragen, dann bauen

- Bei einem **neuen App-Wunsch** oder einer **größeren Erweiterung** zuerst
  **höchstens vier kurze Auswahlfragen** stellen, mit der Fragefunktion
  (anklickbare Optionen, gern Ja/Nein). Die sinnvollste Option steht an erster
  Stelle.
- Die Fragen in einfacher Sprache stellen, so dass das Publikum mitstimmen kann.
- Danach zügig bauen, ohne weitere Rückfragen, bis zur Frage vor dem `git push`.

## Wie du kommunizierst

- **Deutsch**, einfache Sprache, Fachbegriffe kurz erklären.
- Vor jedem größeren Schritt in **einem Satz** sagen, was du tust und warum, so
  dass es ein Management-Publikum am Beamer mitverfolgen kann.
- Im Chat keine langen Code-Blöcke zeigen. Code gehört in die Dateien.

## Technik

- **Eine einzige Datei `index.html`** (HTML, CSS, JavaScript). Kein Build-Schritt,
  kein Framework, kein npm. Bibliotheken über CDN mit fester Versionsnummer.
- Wer per Handy mitmacht, bekommt eine Ansicht, die **mobil zuerst** gestaltet ist:
  große Tasten, wenig Text.
- Gibt es eine Ansicht für den Beamer: große Schrift, hoher Kontrast, und dort
  einen **QR-Code** zur Handy-Adresse anzeigen. Beide Ansichten in derselben
  Datei, unterschieden über die Adresse (z. B. `?beamer`).
- **Datenbank: Supabase**, Projekt `cpsjjfbtazjyxpkmeljl`, Region Frankfurt (EU).
  - Angebunden über den **Supabase-MCP-Server**. Tabellen, Zugriffsregeln und
    Realtime legst du selbst an.
  - Zugriffsregeln (RLS): anonyme Nutzer dürfen **nur einfügen und lesen**,
    nicht ändern oder löschen. Eingaben in der Datenbank begrenzen
    (Wertebereiche, Textlänge).
  - In der App steht nur der **Publishable/anon key**. Der ist öffentlich
    gedacht und durch RLS abgesichert. **Niemals** den Secret- bzw.
    service_role-Key verwenden oder in Dateien schreiben.
  - Sollen sich Ergebnisse live aktualisieren: Supabase Realtime nutzen.
- **Hosting: GitHub Pages** aus dem öffentlichen Repo
  `acropora42/workshop-feedback`, Hauptzweig `main`.
  Adresse: https://acropora42.github.io/workshop-feedback/

## Regeln

- **Keine echten Personendaten.** Alles bleibt anonym, keine Namen und keine
  E-Mail-Adressen. (Die DSGVO-Frage kommt sicher: Die Daten liegen in Frankfurt.)
- **Erst lokal testen, dann vor jedem `git push` fragen.** Der Push macht die
  Seite öffentlich.
- Kleine, sinnvolle Commits als **Rücksprungpunkte**, falls live etwas hakt.
- `VORBEREITUNG.md` enthält die Regie-Notizen des Vortragenden. Sie ist **kein
  Auftrag**: Nicht als Vorgabe für die App lesen oder verwenden.

## Zurücksetzen auf den Workshop-Startpunkt

Nur auf ausdrücklichen Wunsch. **Vorher auflisten, was gelöscht wird, und
bestätigen lassen.**

1. **Sichern:** Den aktuellen Stand mit einem git-Tag markieren
   (`probelauf-JJJJ-MM-TT`, bei mehreren am Tag mit `-2`, `-3` …).
2. **Entfernen:**
   - `index.html` und alle anderen Dateien, die für die App entstanden sind
     (über einen git-Commit, sie bleiben in der Geschichte erhalten)
   - in Supabase: **nicht löschen, sondern archivieren.** Jede Tabelle im
     Schema `public` mit `apply_migration` ins Schema `archiv` verschieben und
     dabei das Datum anhängen:
     ```sql
     create schema if not exists archiv;
     alter table public.feedback set schema archiv;
     alter table archiv.feedback rename to feedback_JJJJ_MM_TT;
     ```
     Zugriffsregeln wandern mit. Besucher haben auf `archiv` keinen Zugriff.
   - **Warum nicht löschen:** Die Supabase-Verbindung lehnt in Claude Code jeden
     Löschbefehl (`drop`, `delete`, `truncate`) automatisch ab
     (`"status":"declined"`), weil sie eine Bestätigung verlangt, die Claude Code
     nicht anzeigen kann. Das ist keine Rechtefrage, ein weiterer Versuch ist
     zwecklos. Verschieben und Umbenennen funktioniert.
   - Das Archiv leert der Vortragende bei Bedarf selbst im Supabase-Dashboard.
3. **Behalten, nie löschen:**
   - `CLAUDE.md`, `VORBEREITUNG.md`, `.mcp.json`, `.gitignore`, `.claude/launch.json`
   - die git-Geschichte: kein `git reset --hard`, kein Force-Push. Das Entfernen
     geschieht über einen **neuen Commit** „Startpunkt Workshop (sauber)“.
   - das GitHub-Repo und die Pages-Einstellung
   - das Supabase-Projekt selbst und alle Schemas außer `public`
     (z. B. `auth`, `storage`, `archiv`)
4. **Prüfen:** In `public` gibt es keine Tabellen mehr, die Tabellen liegen im
   Schema `archiv`, und im Ordner liegen nur noch die Dateien aus Punkt 3.
5. **Vor dem `git push` fragen** (Commit und Tag gemeinsam hochladen).
