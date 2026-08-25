# Deployment: k-deploy → GitHub Pages

Dieses Repository ist **privat**. Der Unterordner `k-deploy/` (in dem diese
Datei liegt) wird automatisch in das **öffentliche** Zielrepo
`JIC-TRIC/k-deploy` (Branch `main`) gepusht und dort über GitHub Pages
ausgeliefert.

**Live-URL:** https://jic-tric.github.io/k-deploy/

## Aktueller Stand

Aktuell wird das Verzeichnis `k-deploy/` **1:1 als statische Seite** deployt.

## Wie der Workflow funktioniert

Definiert in [../.github/workflows/deploy-pages.yml](../.github/workflows/deploy-pages.yml).

> Der Workflow **muss** auf Root-Level unter `.github/workflows/` liegen —
> GitHub Actions erkennt Workflows nur dort. Alles andere Deploy-relevante
> liegt in `k-deploy/`.

**Trigger:**
- Push auf `main`, sofern Dateien in `k-deploy/**` oder der Workflow selbst
  geändert wurden

**Ablauf:**
1. Checkout des privaten Repos
2. Push des Inhalts von `k-deploy/` in `JIC-TRIC/k-deploy@main`
   via `peaceiris/actions-gh-pages@v4`
3. GitHub Pages im Zielrepo liefert den `main`-Branch aus

**Authentifizierung:** SSH-Deploy-Key.
- Privater Schlüssel: Actions-Secret `PAGES_DEPLOY_KEY` in **diesem** Repo.
- Öffentlicher Schlüssel: als Deploy Key mit **Write-Access** im Zielrepo
  `JIC-TRIC/k-deploy`.

`keep_files: false` sorgt dafür, dass alte Dateien im Zielrepo überschrieben
werden – im öffentlichen Repo landen **ausschließlich** die Dateien aus
`k-deploy/`, niemals sonstige Repo-Inhalte des privaten Repos.

## Sicherheit

- Nur der Inhalt von `k-deploy/` landet im öffentlichen Repo.
