# Homelab monitoring (AIO) stack

## What does it contain?

- Grafana
- Grafana Loki
- Grafana Promtail
- syslog-ng
- (InfluxDB) > not impl yet
- (Prometheus)
- (Node exporter)
- (Ping exporter)
- (Blackbox exporter)

## Requirements

- Linux host
- Docker 20.10+

## How to run

1. You need to have installed loki plugin for docker

```
docker plugin install grafana/loki-docker-driver:latest --alias loki --grant-all-permissions
```

2. Enter Loki push URL in `.env`
3. `docker-compose up -d --force-recreate`

### Use Loki-Driver as default log driver

Edit docker daemon config (Linux: /etc/docker/daemon.json / macOS: ~/.docker/daemon.json)

```
{
    "log-driver": "loki",
    "log-opts": {
      "loki-retries": "5",
      "loki-batch-size": "400",
      "loki-url": "http://xxxxxxx:3100/loki/api/v1/push"
    }
}
```

Restart docker daemon.

```
sudo systemctl restart docker
```

## Usefull Links

- https://grafana.com/
- https://labs.lux4rd0.com/2021/01/oldskool-syslog-meets-newskool-loki/
- https://thesmarthomejourney.com/2021/08/23/loki-grafana-log-aggregation/
- https://docs.technotim.live/posts/grafana-loki/
- https://jlovec.net/2021/03/07/collecting-docker-logs-with-loki/
- https://github.com/lpasquali/hell-compose-monitor
- https://github.com/ihyoudou/my-homeserver-metrics-stack

## Trademarks

© Ch. Gross / cflat-inc.org
