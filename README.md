# test-changelog-auto-write

Testprojekt für **Option 1 — Auto Write**.

Der Agent schreibt automatisch einen Changelog-Entwurf in `lib/CHANGELOG.mdx` sobald ein PR mit geänderten Story-Dateien geöffnet wird.

## Ablauf

```
1. Branch erstellen und Story-Datei ändern
2. PR öffnen → Agent schreibt Changelog-Entwurf als Commit
3. Entwickler reviewed CHANGELOG.mdx im PR
4. Merge
```

## Endlosschleifen-Schutz

Der Agent prüft ob der letzte Commit von `github-actions[bot]` stammt.
Falls ja — Action wird übersprungen. Kein erneuter Trigger durch den Bot-Commit.

## Setup

1. `ANTHROPIC_API_KEY` unter **Settings → Secrets → Actions** hinterlegen
2. `.github/workflows/changelog-auto-write.yml` liegt bereits im Repo

## Testen

```bash
git checkout -b test/button-update
# Änderung in lib/components/ui/Button/index.stories.tsx machen
git add .
git commit -m "feat: update Button stories"
git push origin test/button-update
# PR öffnen → Agent startet automatisch
```
