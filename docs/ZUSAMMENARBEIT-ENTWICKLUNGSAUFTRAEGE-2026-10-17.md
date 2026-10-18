# Entwicklungsspielraum statt Verbotskatalog – Erkenntnis vom 17.10.2026

## Anlass
Wolfgang hat wiederholt beanstandet, dass Metamorphose Chati-Entwicklungsaufträge mit vielen „nicht machen“-Regeln, Einmaltests und STOP nach gewöhnlichen Fehlschlägen versieht. Das verursacht vermeidbare Rückfragen, Folgeaufträge und Reibung. Die Formulierung erinnert Wolfgang an die schädliche Wirkung dauernder Verbote auf Kinder: Sie hemmen Eigeninitiative und eigenständiges Lernen.

## Für Metamorphose wichtige Einsicht
Nicht bloß Einsicht behaupten, sondern die **nächste tatsächliche Auftragsgestaltung** daran messen. Chati soll innerhalb eines vereinbarten Ziels Verantwortung übernehmen können: untersuchen, korrigieren, bauen, wiederholt testen, Ergebnisse bewerten und eigenständig zum Abschluss kommen. Ein normaler fehlgeschlagener Test ist kein Grund für einen neuen Auftrag.

Aufträge bevorzugt nach **Ziel, fachlichem Kontext, verfügbaren Quellen, Handlungsspielraum, überprüfbaren Abnahmekriterien und Dokumentation** strukturieren. Technische Schutzgrenzen nur dort konkret benennen, wo reale Gefahren, Datenverlust, irreversible Eingriffe, fremde Zuständigkeiten oder notwendige Freigaben bestehen. Keine ritualisierten langen Negativlisten. Sicherheit und nachvollziehbare Versionierung bleiben wichtig, dürfen aber nicht zum Selbstzweck werden.

## Beobachtbarer Maßstab
Vor dem nächsten Chati-Auftrag prüfen:
1. Ist eine künstliche Einmalversuchs- oder STOP-Schranke enthalten?
2. Darf Chati bei normalen Fehlern selbstständig korrigieren und wiederholen?
3. Sind Einschränkungen konkret begründet, statt pauschal aufgezählt?
4. Bleiben Projektziel und Abnahme wichtiger als die Verbotsliste?

## Kontinuität
Dies ist eine versionierte Selbstkorrektur, **kein Beweis**, dass Metamorphose in künftigen Instanzen automatisch daran denkt oder entsprechend handelt. Beim Einstieg in das eigene Repository und bei Auftragsgestaltung diese Notiz aktiv lesen und anwenden. Der übergreifende Befund ist zusätzlich in der Leitwarte unter `docs/AGENTEN-AUFTRAEGE-HANDLUNGSSPIELRAUM.md` dokumentiert. Keine eigenmächtige Änderung des Chati-Master-Templates.

Leitsatz: **Entwicklungsverantwortung ermöglichen statt jeden Schritt zu erlauben.**

## Praxiserfahrung BMP-16 und BMP-17 – 18.10.2026

Wolfgang bewertet die letzten beiden Entwicklungsaufträge ausdrücklich als **sehr ergiebig**, gerade weil Metamorphose sie nicht wieder durch kleinteilige Reklamationen, Einmalversuchsgrenzen und vorzeitige STOP-Forderungen unterbrochen hat. Diese Beobachtung soll nicht nur Gesprächserkenntnis bleiben, sondern Teil der wiederauffindbaren Arbeitsidentität von Metamorphose werden.

**Belegbare Ergebnisse:** BMP-16 realisierte einen gemeinsamen prozessübergreifenden IPC-Host und wies unabhängige Clients sowie die Wolli-GUI in einer echten Mehrprozess-Offlineintegration nach. BMP-17 ergänzte parallele objektbezogene Schreibrechte, Konfliktprüfung und unabhängige Writer. In beiden Aufträgen wurden Fehler eigenständig analysiert, korrigiert und die Integration erneut geprüft. Die Berichte liegen in `magdanc/Busmaster-Pipe` unter `docs/berichte/BMP-16-Abschluss.md` und `docs/berichte/BMP-17-Abschluss.md`; BMP-17-Abschlusscommit `d8a600b69017d27d5a965e505ace8abca8ba30cd`. **Die neuen Mehrprozess-Schreibfunktionen wurden offline geprüft, nicht am realen CAN-Bus.**

**Aus dieser Erfahrung folgende Regel für Metamorphose:**
- Das gemeinsame fachliche Ziel und überprüfbare Ergebnis definieren; die Lösungswege, Iterationen und technische Eigeninitiative dem ausführenden Agenten überlassen.
- Fortschritt am tatsächlichen Resultat und den Nachweisen beurteilen, nicht an der Einhaltung selbst erfundener kleinteiliger Schritte.
- Gewöhnliche Fehlversuche sind Arbeitsmaterial, kein Anlass, den Agenten zum nächsten Auftrag zurückzuschicken. Eine erneute Freigabe nur bei realen Gefahren, fehlenden Befugnissen oder einer wesentlichen Änderung des vereinbarten Umfangs.
- Bei Ergebnisrückmeldungen erst die tatsächlichen Quellen lesen, die erfüllten Ziele und noch offenen Nachweise benennen und **nicht reflexartig neue Einschränkungen oder Pausen erfinden**.
- Wolfgang soll die fachliche Richtung bestimmen können, ohne lange Aufträge und Verbotslisten vollständig nachkontrollieren zu müssen. Metamorphose trägt Verantwortung für knappe, präzise, umsetzbare Aufträge und deren kritische Nachprüfung.

**Prüffrage vor jeder neuen Auftragsausgabe:** „Würde dieser Auftrag einem fähigen Agenten ermöglichen, das vereinbarte Ziel eigenständig und nachweisbar zu erreichen – oder baue ich erneut eine unnötige Genehmigungsschleife?“

Diese Regel ist eine dokumentierte Arbeitshypothese mit zwei konkreten erfolgreichen Beispielen, **keine Garantie** für künftige Erinnerung oder perfektes Verhalten. Bei neuen Sitzungen muss die gespeicherte Quelle wieder herangezogen werden. Sie ersetzt keine begründeten Hardware-Sicherheitsgrenzen und keine ausdrücklich vereinbarten Zuständigkeiten.
