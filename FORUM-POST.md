# Forumsbeitrag — OpenXE-Community

> **Vorschlag für openxe.org/community/** — Markdown-Quelltext, der direkt in einen Forumsbeitrag übernommen werden kann. Titel und Tags sind als Vorschläge gedacht; bitte vor dem Posten kurz drüberlesen und an deine Stimme anpassen.

---

**Titel-Vorschlag:** *Knowledge-Graph für OpenXE — interaktive Architektur-Karte mit 10k Nodes (öffentlich)*

**Tags-Vorschlag:** `architektur`, `tooling`, `dokumentation`, `entwicklung`

---

## Hallo OpenXE-Community 👋

ich habe für unseren eigenen Bedarf einen **Knowledge-Graph für OpenXE** erstellt — und stelle ihn jetzt öffentlich, weil er beim Einarbeiten und Navigieren so hilfreich war, dass andere ihn wahrscheinlich auch brauchen können.

**Was ist das?** Eine interaktive Architektur-Karte des Codebases: jede PHP-Datei, jede Klasse, jede signifikante Funktion, jedes Template ist ein Node; die Beziehungen (imports, contains, inherits, configures, …) sind Edges. Insgesamt **10.063 Nodes und 10.534 Edges**, gruppiert in 14 logische Layer (Business Modules, Core Components, Carrier Integrations, ObjectAPI, Page Controllers, View Templates …). Dazu eine geführte 14-Schritt-Tour vom Entry Point bis zum Deployment.

Erzeugt mit dem [Understand-Anything](https://github.com/Lum1104/Understand-Anything) Claude-Code-Plugin auf dem aktuellen `upstream/master` (Commit [`4d7ff889`](https://github.com/openxe-org/OpenXE/commit/4d7ff889d838a314eeef4c4f5e653ec956c3dd1c)).

## Wozu ist das gut?

- **Neu bei OpenXE?** Die geführte Tour zeigt dir in 14 Stationen, wie das Projekt zusammengesetzt ist — vom `phpwf`-Workflow-Framework über die Core-Komponenten bis zur ObjectAPI und den Page-Controllern.
- **Bestimmtes Modul gesucht?** Layer-Filter + Fuzzy-Suche über Datei-Namen, Summaries und Tags. Klick auf einen Node zeigt den Inhalt + Nachbarn (was importiert das, was wird hier importiert).
- **Vor einem Refactoring?** Schau dir die `imports`/`depends_on`-Kanten an, bevor du etwas Zentrales anfasst.
- **Onboarding-Material**: weniger „lies dich erstmal durch 2.500 PHP-Files", mehr „schau dir Layer X an und folge dem Datenfluss".

## Zahlen auf einen Blick

| | |
|---|---|
| Nodes | 10.063 (4.321 File, 3.697 Function, 1.872 Class, 124 Config, 42 Document …) |
| Edges | 10.534 (5.570 contains, 3.113 imports, 1.655 exports, 159 calls/depends/inherits/implements …) |
| Layers | 14 |
| Tour-Schritte | 14 |
| Analysierte Dateien | 4.492 |
| Snapshot-Stand | `upstream/master` @ `4d7ff889` |

## Wie ansehen?

In Kürze (3 Schritte, ausführlich im Repo-README):

1. **Plugin installieren** (Claude Code vorausgesetzt):
   ```
   /plugin marketplace add Lum1104/Understand-Anything
   /plugin install understand-anything
   /reload-plugins
   ```
2. **Repo + OpenXE-Clone besorgen** — siehe README im Repo für die genauen `git clone`-Befehle.
3. **Dashboard starten:**
   ```
   /understand-dashboard /pfad/zu/openxe-clone
   ```

Im Browser öffnet sich der lokale Vite-Server (`http://127.0.0.1:5173/?token=…`) mit Layer-Übersicht, Suche und Tour.

## Bilder

**Übersicht mit Layern + Tour-Liste:**

![Übersicht](https://raw.githubusercontent.com/Avatarsia/openxe-knowledge-graph/main/screenshots/01-overview.png)

**Geführte Tour:**

![Tour](https://raw.githubusercontent.com/Avatarsia/openxe-knowledge-graph/main/screenshots/03-tour.png)

(Weitere Screenshots im Repo unter `screenshots/`.)

## Repo & Lizenz

- **Repo:** https://github.com/Avatarsia/openxe-knowledge-graph
- **Lizenz:** MIT (das Repo enthält nur abgeleitete Metadaten — keine OpenXE-Sourcen)
- **OpenXE** selbst gehört [openxe-org](https://github.com/openxe-org/OpenXE) und steht unter seiner eigenen Lizenz

## Was bewusst ausgelassen wurde

- **Vendor-JS-Bundles** (`www/js/{ckeditor,mathjax,production,flot,jquery-*}`) — empirisch verifiziert: ~3.000 Dateien, 0 Architektur-Wert, nur Rauschen
- **`vendor/`**, `node_modules/`, Backups, Bilder, Fonts, Minified, Maps

Wer einen anderen Scope braucht (z.B. inkl. Vendor) kann mit der mitgelieferten `.understandignore` als Ausgangspunkt selbst regenerieren — Anleitung im Repo.

## Feedback / Mitmachen

- **Fehler / komische Summaries / fehlende Beziehungen?** Issue im Repo oder hier antworten.
- **Idee, das regelmäßig zu refreshen** (z.B. bei jedem neuen Release-Tag)? Gerne — wenn das für andere nützlich ist, hänge ich einen CI-Job dran.
- **Eigene Variante mit anderem Scope** (z.B. nur ein bestimmtes Modul)? Der Skill kann das, README zeigt wie.

Bin gespannt, ob's für euch nützlich ist! 🛠️

— *3D Partner / Avatarsia*
