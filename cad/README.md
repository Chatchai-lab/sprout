# cad/

CAD-Modelle, Zeichnungen und Zuschnittlisten der Box (Mechanik). Konstruiert wird mit [FreeCAD](https://www.freecad.org).

## Inhalt

- 3D-Modell der Box (40 × 30 × 50 cm) mit allen Komponenten (M2)
- Zuschnittliste und Zeichnungen mit Maßen (M2)
- Druckdateien für Halterungen (M8, M9)

## Dateien

| Format | Wofür |
| --- | --- |
| `.FCStd` | FreeCAD-Originaldatei, wird weiterbearbeitet |
| `.step` | Austauschformat, öffnet jedes CAD-Programm |
| `.pdf` | Zeichnung mit Maßen, zum Anschauen ohne CAD |
| `.stl` | Druckteile für den 3D-Drucker |

Zu jedem wichtigen Stand neben der `.FCStd` auch eine `.step` und eine `.pdf` ablegen. FreeCAD-Sicherungen (`.FCBak`, `.FCStd1`) werden von Git ignoriert.

## Ablauf mit GitHub Desktop

Einmalig: [GitHub Desktop](https://desktop.github.com) installieren, anmelden, „Clone repository“ → `Chatchai-lab/sprout`.

Danach bei jeder Arbeitssitzung:

1. **Fetch/Pull** klicken, damit der neueste Stand da ist.
2. In FreeCAD arbeiten und im Ordner `cad/` speichern.
3. In GitHub Desktop eine kurze Beschreibung eintragen, z. B. `M2: Elektronikfach ergänzt (#7)`, dann **Commit**.
4. **Push origin** klicken.

## Wichtig

- Eine `.FCStd` ist intern ein ZIP-Archiv. Git kann zwei Versionen davon nicht zusammenführen. Deshalb bearbeitet immer nur eine Person eine CAD-Datei.
- GitHub lehnt Dateien über 100 MB ab. Normale FreeCAD-Dateien sind nur wenige MB groß.
