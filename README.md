# Local Tools

A Docker Compose stack of self-hosted utilities for PDF processing, container management, and network monitoring.

## Services

| Service | Port | Description |
|---|---|---|
| [Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF) | `8080` | PDF toolkit — merge, split, convert, OCR, and more |
| [BentoPDF](https://github.com/alam00000/bentopdf) | `3000` | Lightweight PDF generation |
| [DCM](https://github.com/ajnart/dcm) | `7576` | Docker container manager |
| [NetAlertX](https://github.com/jokob-sk/NetAlertX) | `20211` | Network device monitoring and alerting via ARP scanning |

## Prerequisites

- Docker and Docker Compose

## Quick Start

```sh
cd src
docker compose up -d
```

Access the services at:
- Stirling-PDF: http://localhost:8080
- BentoPDF: http://localhost:3000
- DCM: http://localhost:7576
- NetAlertX: http://localhost:20211

## Configuration

### Environment Variables

NetAlertX is configured via environment variables. Create a `.env` file in `src/` to override defaults:

```env
# Network mode (default: host)
NETALERTX_NETWORK_MODE=host

# Listening address and ports
LISTEN_ADDR=0.0.0.0
PORT=20211
GRAPHQL_PORT=20212
```

### Stirling-PDF

Authentication is disabled by default. To enable it, set `SECURITY_ENABLELOGIN=true` in [docker-compose.yml](src/docker-compose.yml).

Persistent data is stored in `src/stirling-data/`:

```
stirling-data/
├── tessdata/    # OCR language files
├── configs/     # Settings and database
├── logs/        # Application logs
└── pipeline/    # Automation pipeline configs
```

### NetAlertX

Data is stored in a Docker named volume (`netalertx_data`). The container runs in read-only mode with minimal Linux capabilities (`NET_ADMIN`, `NET_RAW`, `NET_BIND_SERVICE`).

## Stopping Services

```sh
cd src
docker compose down
```

To also remove the NetAlertX named volume:

```sh
docker compose down -v
```
