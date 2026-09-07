# Piphi Network Nord Pool

Generated PiPhi integration runtime.

## Run locally

```bash
pdm install -G dev
pdm run uvicorn piphi_network_nord_pool.main:app --reload --port 4214
pdm run pytest
pdm run python scripts/validate.py
```

The runtime listens on port `4214` by default and exposes the common PiPhi runtime route contract:

- `GET /health`
- `GET /diagnostics`
- `POST /discover`
- `POST /config`
- `POST /config/sync`
- `POST /deconfigure`
- `POST /deconfigure/{config_id}`
- `GET /state`
- `GET /contract`
- `GET /entities`
- `GET /events`
- `POST /events/device/{config_id}/example`
- `POST /telemetry/example`
- `POST /telemetry/device/{config_id}/example`
- `POST /command`

## Capability coverage

`capability-catalog.json` inventories area prices, variable market intervals,
daily statistics, price windows, currency conversion, VAT, adjustments,
source health, and chart requirements. Tests enforce that only implemented
capabilities are advertised.

All calculations must use timestamped interval duration rather than assuming
24 hourly values, so hourly and 15-minute market time units, DST days, missing
intervals, and publication delays remain correct.

## Manifest

`manifest.json` is a starter manifest. Before publishing, update:

- `image`
- `version`
- capabilities and commands
- config fields and identity fields
- entity metadata

## Docker

```bash
docker build -t docker.io/piphinetwork/piphi-network-nord-pool:0.1.0 .
docker run --rm -p 4214:4214 docker.io/piphinetwork/piphi-network-nord-pool:0.1.0
```
