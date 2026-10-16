# WSO2 API Manager - Docker

This workspace is prepared to run WSO2 API Manager 4.5.0 with Docker Compose.

## Prerequisites on Windows

1. Enable WSL 2.
2. Install Docker Desktop and use the WSL 2 backend.
3. Start Docker Desktop.

## Start

```powershell
docker compose up -d
```

Watch startup logs:

```powershell
docker compose logs -f wso2-apim
```

Stop the container:

```powershell
docker compose down
```

## Access

- Publisher: https://localhost:9443/publisher
- Developer Portal: https://localhost:9443/devportal
- Carbon Console: https://localhost:9443/carbon
- HTTPS Gateway: https://localhost:8243
- HTTP Gateway: http://localhost:8280

Default local credentials are typically `admin` / `admin`. Change them before using this outside a local development environment.

The first startup can take a few minutes while WSO2 initializes its internal components.

## CREST OpenAPI example

[`crest-openapi.yaml`](./crest-openapi.yaml) documents the HTTP endpoints used by
the deployed [CREST terminal](https://crest-inky.vercel.app/). The public market
response was sampled from the live service; authenticated contracts were inferred
from the deployed client and are marked as an example rather than an official
production contract.

Import the definition in WSO2 Publisher with **Create API → Import Open API** and
select `crest-openapi.yaml`.

The market endpoint can be tested without a login:

```powershell
Invoke-RestMethod "https://crest-inky.vercel.app/api/market/assets?timeframe=30m"
```

The AI, profile, wallet-session, and administration operations depend on CREST's
browser-managed, chunked Supabase authentication. Store the complete Cookie header
in a private Postman environment variable named `crest_cookie_header`; do not put
real cookie values into the OpenAPI file, exported collections, source control, or
terminal history. The OpenAPI definition includes cURL examples for the profile and
AI operations.
