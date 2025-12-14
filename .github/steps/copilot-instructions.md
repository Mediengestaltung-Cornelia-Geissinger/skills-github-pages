## Kurzüberblick

Dieses Repository ist ein GitHub Pages / Jekyll Lern-Template (eine Schritt-für-Schritt-„course template“).
Zweck: die Lernschritte in `README.md` automatisiert über GitHub Actions vorantreiben und eine einfache `my-pages`-Seite erzeugen.

## Große Architektur (big picture)
- Content: Haupt-UX lebt in [README.md](README.md) und den Markdown-Dateien unter `.github/steps/`.
- Laufzeit / CI: sechs kleine, step-getriggerte Workflows in `.github/workflows/` (z. B. `0-welcome.yml` ... `5-merge-your-pull-request.yml`).
- Step-Koordination: die Datei `.github/steps/-step.txt` hält die aktuelle Schritt-Nummer; Workflows lesen sie und laufen nur für passende Schritte.

## Wichtige Patterns & Konventionen
- Branch: Workflows nutzen die Branch-Konvention `my-pages` (wird in Actions als Ziel-Branch referenziert). Ändere sie nicht ohne die Workflows anzupassen.
- Step-Updates: Verwende `skills/action-update-step@v2` mit `from_step` / `to_step` / `branch_name` (schau Beispiele in den Workflow-Dateien).
- Pages-Build: Workflows reagieren u.a. auf `page_build` und auf Pushes in `my-pages` (z. B. `index.md`, `_config.yml`, `_posts/*.md`).
- Posts: Blog-Posts gehören nach `_posts/` und matchen `*_posts/*.md` für Step-Erkennung.

## Änderungs- und Prüfregeln
- Sicherheits- / Template-Check: Workflows prüfen `!github.event.repository.is_template` — sei vorsichtig, wenn du Logik für Template-Repos änderst.
- Tests / Verifikation: Es gibt keine lokalen Tests; validiere Änderungen durch manuelles Triggern von Workflows (`Actions` -> `Run workflow`) oder durch Push/PRs, die die jeweiligen Events auslösen.

## Konkrete Beispiele (Was zu editieren ist)
- Neue Startseite erstellen: Erstelle `_config.yml` und `index.md` auf Branch `my-pages`. Workflows erstellen Branch/PRs in der `0-welcome.yml`-Action.
- Step erweitern: Wenn du einen neuen Schritt hinzufügst, aktualisiere:
  - `.github/steps/` (neues Markdown für die Anleitung und die Schrittdatei),
  - alle Workflows, die `from_step`/`to_step` erwarten,
  - die Referenzen im `README.md` (die README-Kommentare enthalten step-Inhalte).

## Hinweise für AI-Codieragenten
- Mache minimale, zielgerichtete Änderungen; die Workflows sind bewusst klein und sequenziell — verändere Branch-/Event-Logik nur wenn nötig.
- Prüfe `.github/steps/-step.txt` und die `if:`-Bedingungen in den Workflows, bevor du automationskritische Änderungen vornimmst.
- Verweise in PR-Beschreibungen auf die geänderten Step-Nummern (z. B. "Update step 3 → 4 in README and workflow 3-customize-your-homepage.yml").

## Dateien zum Ansehen
- [README.md](README.md) — Haupt-Inhalt und Schritt-Anweisungen
- [.github/workflows/](.github/workflows/) — Schritt-Workflows (0..5)
- [.github/steps/](.github/steps/) — Markdown-Anleitungen pro Schritt und `-step.txt`

Wenn etwas unklar ist oder du weitere Beispiele wünschst, sag mir, welche Änderung du vorhast und ich ergänze die Anweisungen oder passe die Datei an.
