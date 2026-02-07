# OpenAPI Spec

[![Sync](https://github.com/stempapp/openapi/actions/workflows/sync-openapi.yml/badge.svg)](https://github.com/stempapp/openapi/actions/workflows/sync-openapi.yml)
[![Validate](https://github.com/stempapp/openapi/actions/workflows/validate-openapi.yml/badge.svg)](https://github.com/stempapp/openapi/actions/workflows/validate-openapi.yml)

Automatisch synchronisierte OpenAPI-Spezifikation der stemp Production API.
Grundlage für die automatische SDK-Generierung.

## Wie es funktioniert

```
Production API ──[03:00 CET]──▸ GitHub Actions ──▸ openapi.json ──▸ SDKs
```

| Was | Details |
|-----|---------|
| **Sync-Zyklus** | Täglich um 03:00 Uhr CET |
| **Quelle** | Production API (URL als Secret hinterlegt) |
| **Format** | OpenAPI 3.x, pretty-printed & key-sorted JSON |
| **Validierung** | Spectral Linting bei jedem Push |

## Setup

### 1. GitHub Secret anlegen

Das Repository benötigt ein Secret mit der API-URL:

```
Repository Settings → Secrets and variables → Actions → New repository secret
```

| Name | Wert |
|------|------|
| `OPENAPI_URL` | Die vollständige URL zum OpenAPI-Endpoint |

### 2. Manueller Sync

Der Workflow kann jederzeit manuell ausgelöst werden:

```
Actions → Sync OpenAPI Spec → Run workflow
```

## Für SDK-Generierung

Die `openapi.json` kann als Quelle für Code-Generatoren verwendet werden:

```bash
# Beispiel mit openapi-generator
npx @openapitools/openapi-generator-cli generate \
  -i https://raw.githubusercontent.com/stempapp/openapi/main/openapi.json \
  -g typescript-axios \
  -o ./sdk

# Beispiel mit orval
npx orval --input https://raw.githubusercontent.com/stempapp/openapi/main/openapi.json
```

## Spec lokal anschauen

```bash
# Mit Swagger UI
npx @redocly/cli preview openapi.json

# Oder direkt im Browser
npx swagger-ui-watcher openapi.json
```
