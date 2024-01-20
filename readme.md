# FastAPI with Observability

Observe the FastAPI application with three pillars of observability on [Grafana](https://github.com/grafana/grafana):

1. Traces with [Tempo](https://github.com/grafana/tempo) and [OpenTelemetry Python SDK](https://github.com/open-telemetry/opentelemetry-python)
2. Metrics with [Prometheus](https://prometheus.io/) and [Prometheus Python Client](https://github.com/prometheus/client_python)
3. Logs with [Loki](https://github.com/grafana/loki)


## Quick Start

1. Install [Loki Docker Driver](https://grafana.com/docs/loki/latest/clients/docker-driver/)

   ```bash
   docker plugin install grafana/loki-docker-driver:latest --alias loki --grant-all-permissions
   ```

2. Start all services with docker-compose

   ```bash
   docker-compose up -d
   ```

   If got the error message `Error response from daemon: error looking up logging plugin loki: plugin loki found but disabled`, please run the following command to enable the plugin:

   ```bash
   docker plugin enable loki
   ```

3. Send requests with [siege](https://linux.die.net/man/1/siege) and curl to the FastAPI app

   ```bash
   bash request-script.sh
   bash trace.sh
   ```

   Or you can use [Locust](https://locust.io/) to send requests:

   ```bash
   # install locust first with `pip install locust` if you don't have it
   locust -f locustfile.py --headless --users 10 --spawn-rate 1 -H http://localhost:8000
   ```

   Or you can send requests with [k6](https://k6.io/):

   ```bash
   k6 run --vus 1 --duration 300s k6-script.js
   ```
