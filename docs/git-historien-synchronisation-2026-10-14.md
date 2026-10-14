# Bericht: Erhalt lokaler Git-Historien bei GitHub-Synchronisation

Datum: 14. Oktober 2026  
Repository: [magdanc/Metamorphose](https://github.com/magdanc/Metamorphose)  
Status: Verfahren dokumentiert; lokaler Git-Transport noch nicht praktisch qualifiziert.

## Ausgangslage und Bewertung

Für eine **unveränderte Übernahme bestehender lokaler Commit-Historien** wird regulärer Git-Transport über HTTPS oder SSH benötigt. Der zuvor nachgewiesene [GitHub-Integrations-Schreibzugriff](github-integration-bericht-2026-10-14.md) belegt **nicht** diesen Transportweg.

Die vorhandenen Integrationswerkzeuge können Dateien, Trees, Commits und Branch-Verweise auf GitHub erzeugen. Das angebotene Commit-Werkzeug übernimmt jedoch nicht sämtliche Originaldaten eines bestehenden lokalen Git-Commits. Ein Nachbau über die Integration gewährleistet deshalb keine unveränderten Commit-IDs. Die allgemeine [GitHub-API zum Erstellen von Commits](https://docs.github.com/en/rest/git/commits#create-a-commit) ist von den konkret verfügbaren Integrationswerkzeugen zu unterscheiden.

Lokal ist Git **2.56.0.windows.2** vorhanden. Eine erfolgreiche Authentifizierung für lokalen Git-Transport zu GitHub wurde noch nicht nachgewiesen; sie ist unabhängig von der GitHub-Integration.

## Wiederholbarer Synchronisationsweg

### 1. Voraussetzungen und Sicherung

Vorausgesetzt werden ein vollständiges lokales Repository, ein sauberer Arbeitsstand, ein ausdrücklich benannter Zielbranch und funktionierende Git-Zugangsdaten. Während der Synchronisation darf kein zweiter Agent das betreffende Repository verändern.

PowerShell-Beispiel mit **vor Ausführung anzupassenden Platzhaltern**:

```powershell
$repo = 'C:\Pfad\zum\Projekt'
$url = 'https://github.com/OWNER/REPOSITORY.git'
$branch = 'main'
$backup = "C:\Pfad\zu\Sicherungen\Projekt-$(Get-Date -Format yyyyMMdd-HHmmss).bundle"

git -C $repo status --porcelain=v1 --untracked-files=all
git -C $repo branch --show-current
git -C $repo rev-parse --is-shallow-repository
$head = git -C $repo rev-parse HEAD
git -C $repo remote -v
```

**STOP**, wenn Dateien geändert oder unversioniert sind, der Branch nicht dem vorgesehenen Stand entspricht, das Repository unvollständig oder shallow ist oder einer der Befehle fehlschlägt. Insbesondere dürfen Fehler nicht als leerer Arbeitsstand interpretiert werden.

Nach positiver Vorprüfung ein Bundle an einem neuen, bestehenden Sicherungsziel erstellen und prüfen:

```powershell
git -C $repo bundle create $backup --all
git -C $repo bundle verify $backup
```

Ein Git-Bundle sichert die über Git-Referenzen erreichbare Historie; uncommittete Dateien und Git-LFS-Nutzdaten sind nicht darin enthalten. Siehe [Git-Bundle](https://git-scm.com/docs/git-bundle).

### 2. GitHub-Stand prüfen

```powershell
git -C $repo ls-remote --exit-code --heads $url "refs/heads/$branch"
```

Exitcode **0**: Zielbranch vorhanden. Exitcode **2**: Kein passender Zielbranch. Andere Fehler – gerade Anmeldefehler – bedeuten **nicht**, dass GitHub leer ist.

Wenn der Branch vorhanden ist:

```powershell
git -C $repo fetch --no-tags $url "refs/heads/$branch"
$remoteHead = git -C $repo rev-parse FETCH_HEAD
git -C $repo rev-list --left-right --count "$head...$remoteHead"
git -C $repo log --oneline --left-right "$head...$remoteHead"
```

`fetch` holt Objekte, ohne den ausgecheckten Arbeitsstand zusammenzuführen. Siehe [Git-Fetch](https://git-scm.com/docs/git-fetch).

| Nur lokal / nur entfernt | Bewertung und Folge |
|---|---|
| `0 / 0` | Bereits synchron. |
| `>0 / 0` | Regulärer Fast-Forward-Push ist möglich. |
| `0 / >0` | GitHub-Änderungen prüfen, dann gezielt `git merge --ff-only $remoteHead`; anschließend erneut vorprüfen. |
| Beides `>0` | **STOP**; gemeinsame Basis und Zusammenführung gesondert entscheiden. |
| Zielbranch fehlt | Neuanlage des Branches ausdrücklich bestätigen; bestehende lokale Historie bleibt übernehmbar. |

Bei divergierenden Historien kann ein normaler Merge beide Linien erhalten. Rebase und Squash verändern bestehende Commit-IDs und sind für dieses Erhaltungsziel nicht geeignet. Unabhängige Historien nicht erzwingen. Siehe [Git-Merge](https://git-scm.com/docs/git-merge).

### 3. Push nur nach ausdrücklicher Freigabe

Unmittelbar vor dem Push lokalen HEAD und entfernten Branch nochmals prüfen. Bei jeder Änderung gegenüber der Vorprüfung: **STOP**, neu bewerten.

Nach gesonderter Freigabe:

```powershell
git -C $repo -c push.followTags=false push $url "${head}:refs/heads/$branch"
```

Dieser Befehl überträgt den geprüften Commit mitsamt seiner erreichbaren Vorgeschichte. Kein `--force`, kein `--mirror`. Ein regulärer Push verweigert das Überschreiben einer zwischenzeitlich abweichenden entfernten Historie. Andere Branches und Tags erfordern eigene Freigaben. Siehe [Git-Push](https://git-scm.com/docs/git-push).

Danach:

```powershell
git -C $repo rev-parse HEAD
git -C $repo ls-remote --exit-code --heads $url "refs/heads/$branch"
```

Lokaler und entfernter HEAD müssen exakt dem freigegebenen `$head` entsprechen. Ziel-URL, Branch, Ausgangsstände und Resultat-SHA werden protokolliert.

## Rückkehr und Sonderfälle

Das geprüfte Bundle kann unabhängig in einem **neuen Ordner** wiederhergestellt werden: `git clone <Bundlepfad> <neuer-Ordner>`. Ein laufender Konflikt-Merge kann mit `git merge --abort` beendet werden. Bereits veröffentlichte Änderungen werden nach gesonderter Freigabe per Rücknahme-Commit korrigiert, ohne gemeinsam genutzte Historie umzuschreiben.

Bei Git LFS und Submodulen sind zusätzlich die LFS-Nutzdaten beziehungsweise referenzierten Submodule und deren Zugänge gesondert zu sichern und zu prüfen.

## Grenzen des Nachweises

- **Belegt:** GitHub-Integration kann gezielt Dateien und Commits über die API schreiben (separater Bericht).
- **Festgelegt, noch nicht praktisch qualifiziert:** Regelmäßiger lokaler Git-Transport für unveränderte Commit-Historien.
- **Nicht durchgeführt:** Lokaler Push, Rechteänderungen, Eingriffe in bestehende Projekt-Repositories.
- Ein API-Commit ist **kein** Nachweis für lokale Git-Authentifizierung oder einen erfolgreichen Git-Push.

Dieser Bericht bewahrt das erarbeitete Verfahren als dauerhafte Dokumentation, ohne einen noch ausstehenden Praxistest als abgeschlossen darzustellen.
