<div align="center">
  <img src="docs/static/logo.png" alt="Air You Dying For" width="120" style="filter:invert(1)">
  <h1>Air You Dying For</h1>
</div>

[![Build](https://github.com/just5ky/Air-You-Dying-For/actions/workflows/docker-build-push.yml/badge.svg)](https://github.com/just5ky/Air-You-Dying-For/actions/workflows/docker-build-push.yml)
[![Image](https://img.shields.io/badge/ghcr.io-air--you--dying--for-0d1117?logo=docker&logoColor=white)](https://github.com/just5ky/Air-You-Dying-For/pkgs/container/air-you-dying-for)
[![Site](https://img.shields.io/badge/website-just5ky.github.io-7c3aed?logo=github&logoColor=white)](https://just5ky.github.io/air-you-dying-for/)

CO2, temperature, and humidity monitor using the SCD41 sensor on Raspberry Pi 4. Exposes metrics via Prometheus.

## Hardware

- Raspberry Pi 4
- [Sensirion SCD41](https://sensirion.com/products/catalog/SCD41/) via I2C

## Metrics

| Metric | Description |
|---|---|
| `co2_ppm` | CO2 level in PPM |
| `temperature_celsius` | Temperature in Celsius |
| `humidity_percent` | Relative humidity in percent |

## Quick Start

### Prerequisites

Enable I2C on the Pi:
```bash
sudo raspi-config  # Interface Options → I2C → Enable
```

Verify i2c group GID (needed for compose):
```bash
getent group i2c | cut -d: -f3
```
Update `group_add` in [docker-compose.yml](docker-compose.yml) if it differs from `995`.

### Run with Docker Compose

```bash
# Build and run locally
docker compose up -d

# Or pull from GHCR
GITHUB_REPOSITORY_OWNER=just5ky docker compose up -d
```

### Environment Variables

| Variable | Default | Description |
|---|---|---|
| `PROMETHEUS_PORT` | `8000` | Port to expose Prometheus metrics |

## Container Image

Multi-arch image (`linux/arm64`, `linux/arm/v7`) published to GHCR on every push to `main` and on version tags.

```bash
docker pull ghcr.io/just5ky/air-you-dying-for:latest
```

## Development

```bash
pip install -r requirements.txt
python scd41_monitor.py
```
