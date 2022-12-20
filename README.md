# OpenWeather Exporter

![Docker Pulls](https://img.shields.io/docker/pulls/billykwooten/openweather-exporter.svg)
![Docker Automated](https://img.shields.io/docker/cloud/automated/billykwooten/openweather-exporter.svg)
[![report](https://goreportcard.com/badge/github.com/billykwooten/openweather-exporter)](https://goreportcard.com/report/github.com/billykwooten/openweather-exporter)
![Docker Build](https://img.shields.io/docker/cloud/build/billykwooten/openweather-exporter.svg)
[![license](https://img.shields.io/github/license/billykwooten/openweather-exporter.svg)](https://github.com/billykwooten/openweather-exporter/blob/main/LICENSE)
[![release](https://img.shields.io/github/release/billykwooten/openweather-exporter/all.svg)](https://github.com/billykwooten/openweather-exporter/releases)

Prometheus exporter for [openweather API](https://openweathermap.org/api)

## Requirements

* Linux / MacOSX, [`git bash`](https://git-scm.com/download/win) for Windows
* [docker](https://www.docker.com)

## Development

* [go](https://golang.org/dl)
* [openweathermap](https://github.com/briandowns/openweathermap)

## Configuration

OpenWeather exporter can be controlled by both ENV or CLI flags as described below.

| Environment         | CLI (`--flag`)   | Default        | Description                                                                                                                   |
|---------------------|------------------|----------------|-------------------------------------------------------------------------------------------------------------------------------|
| `OW_LISTEN_ADDRESS` | `listen-address` | `:9091`        | The port for /metrics to listen on                                                                                            |
| `OW_APIKEY`         | `apikey`         | `<REQUIRED>`   | Your Openweather API key                                                                                                      |
| `OW_CITY`           | `city`           | `New York, NY` | City/Location in which to gather weather metrics. Separate multiple locations with \| for example "New York, NY\|Seattle, WA" |
| `OW_DEGREES_UNIT`   | `degrees-unit`   | `F`            | Unit in which to show metrics (Kelvin, Fahrenheit or Celsius)                                                                 |
| `OW_LANGUAGE`       | `language`       | `EN`           | Language in which to show metrics                                                                                             |

## Usage

Binary Usage

``` bash
# Export weather metrics from Seattle using binary
./openweather-exporter --city "Seattle, WA" --apikey mi4o2n54i0510n4510
```

Docker Usage

``` bash
# Export weather metrics from Seattle using docker
docker run -d --restart on-failure --name=openweather-exporter -p 9091:9091 arnoldthebat/openweather-exporter --city "Seattle, WA" --apikey mi4o2n54i0510n4510
```

Docker-compose Usage

``` bash
  openweather-exporter:
    image: arnoldthebat/openweather-exporter
    container_name: openweather-exporter
    restart: always
    ports:
      - "9091:9091"
    environment:
      - OW_CITY=New York, NY
      - OW_APIKEY=mi4o2n54i0510n4510
```

Prometheus Scrape Usage

``` bash
scrape_configs:
  - job_name: 'openweather-exporter'
    scrape_interval: 60s
    static_configs:
      - targets: ['openweather-exporter:9091']
```

## Grafana

I have created a grafana dashboard for this exporter, feel free to use it. Link below.

[Dashboard Link](https://github.com/billykwooten/GrafanaDashboards/blob/master/open_weather_map.json)

## Notes

If you'd like to build this yourself you can clone this repo and run:

``` bash
./script/cibuild
```

<!-- cSpell:ignore cibuild, openweather, apikey, arnoldthebat, openweathermap -->