<p align="center">
  <img src="https://cdn.stemp.app/logo/color.svg" alt="stemp" height="64" />
</p>

<h3 align="center">OpenAPI Spec</h3>

<p align="center">
  Automatisch synchronisierte OpenAPI-Spezifikation der stemp API.<br/>
  Grundlage für die automatische SDK-Generierung.
</p>

<p align="center">
  <a href="https://github.com/stempapp/openapi/actions/workflows/sync-openapi.yml"><img src="https://github.com/stempapp/openapi/actions/workflows/sync-openapi.yml/badge.svg" alt="Sync" /></a>
  <a href="https://github.com/stempapp/openapi/actions/workflows/validate-openapi.yml"><img src="https://github.com/stempapp/openapi/actions/workflows/validate-openapi.yml/badge.svg" alt="Validate" /></a>
</p>

---

## Wie es funktioniert

```
Production API ──[03:00 CET]──▸ GitHub Actions ──▸ openapi.json ──▸ SDKs
```

| Was | Details |
|-----|---------|
| **Sync-Zyklus** | Täglich um 03:00 Uhr CET |
| **Format** | OpenAPI 3.x, pretty-printed & key-sorted JSON |
| **Validierung** | Spectral Linting bei jedem Push |
| **Trigger** | Automatisch (Schedule) oder manuell (Actions → Run workflow) |

## SDK-Generierung

Die `openapi.json` kann direkt als Quelle für Code-Generatoren verwendet werden:

```bash
# openapi-generator
npx @openapitools/openapi-generator-cli generate \
  -i https://raw.githubusercontent.com/stempapp/openapi/main/openapi.json \
  -g typescript-axios \
  -o ./sdk

# orval
npx orval --input https://raw.githubusercontent.com/stempapp/openapi/main/openapi.json
```

## Spec lokal anschauen

```bash
# Swagger UI
npx @redocly/cli preview openapi.json

# Oder direkt im Browser
npx swagger-ui-watcher openapi.json
```
