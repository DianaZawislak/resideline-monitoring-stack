# Monitoring Server Setup

This server runs a comprehensive monitoring stack using Docker Compose, including Prometheus, Grafana, Loki, and other supporting services.

## Components

- **Prometheus**: Metrics collection and storage
- **Grafana**: Visualization and dashboarding (custom build with MongoDB plugin)
- **Loki**: Log aggregation system
- **Promtail**: Log shipping agent for Loki
- **cAdvisor**: Container monitoring

## Directory Structure

```
monitoring/
├── docker-compose-full.yml
├── Dockerfile
├── prometheus.yml
├── loki-config.yaml
├── promtail-config.yaml
├── grafana-config/
└── grafana-data/
```

## Starting the Stack

To start the monitoring stack:

```bash
cd /root/monitoring
docker-compose -f docker-compose-full.yml up -d
```

## Accessing Services

- Grafana: `http://server-ip:3000`
- Prometheus: `http://server-ip:9090`
- Loki: `http://server-ip:3100` (typically accessed through Grafana)

## Configuration Files

- `docker-compose-full.yml`: Defines all services and their configurations
- `Dockerfile`: Custom Grafana image with MongoDB plugin
- `prometheus.yml`: Prometheus configuration
- `loki-config.yaml`: Loki configuration
- `promtail-config.yaml`: Promtail configuration for log shipping

## Grafana

- Custom build with MongoDB plugin
- Data persisted in `./grafana-data`
- Configuration stored in `./grafana-config`

## Updating

To update the stack:

1. Pull the latest images:
   ```bash
   docker-compose -f docker-compose-full.yml pull
   ```
2. Rebuild custom images:
   ```bash
   docker-compose -f docker-compose-full.yml build
   ```
3. Restart the stack:
   ```bash
   docker-compose -f docker-compose-full.yml up -d
   ```

## Backups

Regular backups of the following directories are recommended:
- `/root/monitoring/grafana-data`
- `/mnt/volume_nyc3_01_monitoring/prometheus_data`

## Troubleshooting

- Check container logs:
  ```bash
  docker-compose -f docker-compose-full.yml logs [service_name]
  ```
- Restart a specific service:
  ```bash
  docker-compose -f docker-compose-full.yml restart [service_name]
  ```
- Rebuild and recreate containers:
  ```bash
  docker-compose -f docker-compose-full.yml up -d --force-recreate --build
  ```

## Additional Notes

[Add any specific notes about your setup, custom configurations, or important reminders here]
