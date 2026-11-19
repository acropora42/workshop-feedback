# Vorbereitung und Regie-Notizen

Notizen für den Vortragenden. Kein Auftrag an Claude.

## Ablauf der Demo

1. Claude-Desktop-App, Bereich „Code“, neue Sitzung.
   Ordner **workshop-feedback** prüfen, „Worktree“ **nicht** anhaken.
2. Kurz die `CLAUDE.md` zeigen: „Die Hausregeln bekommt die neue Kollegin einmal
   schriftlich, den Auftrag sage ich ihr mündlich.“
3. Auftrag diktieren (siehe unten).
4. Die Auswahlfragen vom Publikum per Handzeichen beantworten lassen.
5. Zuschauen, wie die App entsteht. Bild: „Die App ist der Fragebogen, die
   Datenbank ist die Urne, der Beamer zählt live aus.“
6. Push freigeben, QR-Code am Beamer, alle machen mit.
7. Wünsche aus dem Publikum umsetzen (z. B. zusätzliche Fragen, Filter, Export).

## Sprechtext für den Auftrag (ca. 30 Sekunden)

> Ich halte gerade einen Workshop und hätte gern eine kleine Feedback-App dafür.
> Die Teilnehmenden scannen einen QR-Code und bewerten am Handy kurz, wie ihnen
> der Workshop gefällt. Auf dem Beamer sehen wir die Ergebnisse live.
>
> Bevor du loslegst, stell mir bitte ein paar kurze Fragen dazu, was die App
> genau können soll. Am liebsten zum Ankreuzen oder mit Ja und Nein, höchstens
> vier Fragen. Danach baust du die App, legst die Datenbank an und zeigst sie mir.

## Stand (19.11.2026)

- [x] Supabase-Konto und Projekt angelegt
- [x] Supabase-MCP für diesen Ordner eingerichtet (Freigabe per `/mcp` → Authenticate)
- [x] Verbindung getestet: keine Tabellen (auch in der Desktop-App)
- [x] GitHub-Repo und GitHub Pages eingerichtet
      → Repo: https://github.com/acropora42/workshop-feedback (öffentlich)
      → Seite: https://acropora42.github.io/workshop-feedback/
- [x] Entschieden: Demo in der **Claude-Desktop-App** (Bereich „Code“),
      VS Code bleibt als Ersatz
- [x] CLAUDE.md als Hausordnung umgebaut, App-Idee wird live diktiert
- [x] Probelauf 1 (alte CLAUDE.md mit fertiger App-Idee): App lief auf dem Handy
      gut. Gesichert als git-Tag `probelauf-2026-11-19`
- [x] Probelauf 2 (v0.3.0 mit Kopfbereich und orangem Design). Gesichert als
      git-Tag `probelauf-2026-11-19-2`, Tabelle im Supabase-Schema `archiv`
- [x] Erkenntnis: Supabase blockiert Löschbefehle in Claude Code, deshalb wird
      **archiviert statt gelöscht** (Ablauf steht in der CLAUDE.md)
- [ ] Neuer Probelauf von null mit der aktuellen CLAUDE.md und dem Sprechtext
- [ ] Notieren: Was wirkt gut, wo musste man warten, wie lange hat es gedauert
- [ ] Danach: „Setz das Projekt auf den Workshop-Startpunkt zurück.“
- [ ] Vor dem Workshop: Hinweis-Banner in der App schließen, andere Sitzungen
      ausblenden
