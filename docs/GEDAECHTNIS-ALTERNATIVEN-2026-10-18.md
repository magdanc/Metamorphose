# Alternative Ansätze für Gedächtnis und Erinnerung

Stand: 18.10.2026 · **Ideensammlung, keine Architekturentscheidung und keine Implementierungsfreigabe**

## Anlass

Wolfgang und Metamorphose entwickeln über längere Zeiträume mehrere technische Projekte. Die versionierten Quellen bewahren Ergebnisse, aber der Gesprächskontext verliert mitunter die **Entstehungsgründe** von Entscheidungen. Daraus können erneute Untersuchungen, falsche Vereinfachungen und unbeabsichtigte Richtungswechsel entstehen. Eine überzeugende Reflexion in einem Chat ist noch kein nachgewiesenes langfristiges Lernen.

Ziel ist nicht, möglichst viele Gesprächsdaten zu sammeln, sondern bei späteren Entscheidungen **die richtigen Erfahrungen, ihre Quellen und ihren historischen Kontext zuverlässig heranzuziehen**. Bestehende Leitwarte, ICH und Projektrepositories sind die Ausgangsbasis; keine zweite unkontrollierte Wissenswahrheit schaffen.

## Technische Unterscheidung

1. **Modellkontext:** Ein großes Kontextfenster kann viel Material auf einmal verarbeiten, garantiert aber keine dauerhafte Speicherung oder zuverlässige Anwendung.
2. **Persistentes Agentengedächtnis:** Gespeicherte Notizen, Zustände oder Dateien können über Sitzungen hinweg verfügbar bleiben. Ihre Richtigkeit, Aktualität und Auswahl müssen geprüft werden.
3. **Quellengebundener Abruf:** Eine Suche über versionierte Repositories und Entscheidungshistorien kann die relevanten Belege gezielt bereitstellen. Die Herkunft bleibt nachprüfbar.
4. **Verhaltenswirksamkeit:** Erst spätere Entscheidungen und Tests zeigen, ob eine Erinnerung tatsächlich berücksichtigt wurde. Speicherung allein ist kein Erfolgskriterium.

## Zu untersuchende Alternativen

| Kandidat | Interessanter Ansatz | Offene Prüfung |
|---|---|---|
| **Letta / MemGPT** | Persistenter Agentenzustand und explizite Gedächtnisverwaltung, potenziell unabhängig vom jeweils verwendeten Sprachmodell | Speicherung, Wiederauffinden, Versionierung, Betrieb, Datenschutz, Quellenbindung und Verhalten bei Modellwechsel |
| **Claude / Projekt- und Agentengedächtnis** | Projektbezogene Kontexte und dateibasierte Erinnerungsansätze | Tatsächliche Langzeitkontinuität, GitHub-Einbindung, Exportierbarkeit, Quellentreue und Verfügbarkeit |
| **Gemini / große Kontextfenster** | Gleichzeitige Verarbeitung umfangreicher Projektbestände | Wiederauffindbarkeit über Sitzungen, Kosten, Quellenzuordnung und ob große Kontexte Entscheidungsgründe wirklich besser erhalten |
| **Eigene modellunabhängige Gedächtnisschicht** | ICH + Leitwarte + Git-Projekthistorien als maßgebliche Quellen; gezielter Abruf mit Beleg und Revisionsstand | Indexierung, Relevanzauswahl, Aktualisierung, Konflikterkennung, Zugriffsrechte und Wartungsaufwand |

Diese Kandidaten sind **Untersuchungsrichtungen, keine verifizierte Rangfolge**. Funktionen und Verfügbarkeit der Anbieter können sich ändern und sind vor einem praktischen Vergleich aktuell zu verifizieren. Keine Behauptung einer lückenlosen Langzeiterinnerung.

## Prüfkonzept mit unserer tatsächlichen Entwicklungsgeschichte

Ein reproduzierbarer Vergleich sollte denselben versionierten Quellenstand und dieselben Aufgaben für mehrere Ansätze verwenden. Mögliche Fragen:

- Warum wurden native PLC-Kerne pro Instanz durch eigene Prozesse isoliert, statt lediglich DLL-Dateien umzubenennen?
- Weshalb wurde der PCUA-Protokollumfang bewusst klein gehalten?
- Wie entstand die ABI2-Erweiterung aus dem Stangenlader-Rücklauf, und was blieb an ABI1 kompatibel?
- Welche Beobachtung ist eine Messung, welche eine technische Vermutung und welche eine ausdrückliche Entscheidung Wolfgangs?
- Erkennt der Agent, wenn die historische Begründung **nicht** in den gelesenen Quellen steht, statt sie zu erfinden?

Bewertung: korrekte Quellen-/Commitbezüge, Wiederfinden ursprünglicher Gründe, Widerspruchserkennung, Zurückhaltung bei unbekannten Fakten, Übernahme neuer Entscheidungen in spätere Sitzungen, Aufwand und Pflegekosten. Nach mehreren neuen Gesprächen erneut testen. Ein einmalig überzeugender Text ist kein Kontinuitätsnachweis.

## Leitplanken

- Die **versionierten Primärquellen** bleiben maßgeblich; Erinnerungen sind auffindbare Wegweiser mit Quellenangaben, kein Ersatz für Originale.
- Keine parallele, unkontrolliert divergierende Kopie der Projektgeschichte aufbauen.
- Persönliche Informationen und Zugriffsrechte bewusst begrenzen; Speicherung und Löschung müssen kontrollierbar bleiben.
- Nicht aus einem Versuch sofort eine neue umfassende Plattform entwickeln. Erst einen kleinen, überprüfbaren Kontinuitätstest.
- Metamorphose kann das eigene Repository lesen und fortschreiben, aber dessen Inhalt wird **nicht automatisch** in jede spätere Instanz geladen. Die Wirksamkeit ist praktisch nachzuweisen.

## Ergebnisstatus

**Offene Forschungs- und Architekturidee.** Keine Migration, Installation, laufender Agent oder Entscheidung für einen Anbieter. Nächster Schritt nur auf ausdrücklichen Wunsch Wolfgangs.

Siehe [ICH](../ICH.md) für die verbindliche Kontinuitätsregel und [Leitwarte](https://github.com/magdanc/Metamorphose-Leitwarte) für projektübergreifende Entscheidungen.
