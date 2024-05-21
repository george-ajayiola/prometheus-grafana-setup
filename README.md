To enable the lifecycle HTTP endpoints in your Prometheus container using Docker Compose, you need to add the --web.enable-lifecycle flag to the command section of your docker-compose.yml file.

Here's your updated docker-compose.yml file:
```
version: '3.8'
services:
  prometheus:
    image: prom/prometheus
    container_name: prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--web.enable-lifecycle'
    ports:
      - 9090:9090
    restart: unless-stopped
    volumes:
      - ./prometheus:/etc/prometheus
      - prom_data:/prometheus
volumes:
  prom_data:
```
Reload the Prometheus configuration without restarting:
```
curl -X POST http://localhost:9090/-/reload
```
