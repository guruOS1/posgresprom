
TODO: 
- run postgres
- monitor with prometheus-postgres-exportter


# Run postgres 
docker run -d \
    --name some-postgres \
    -e POSTGRES_PASSWORD=mysecretpassword \
    -e PGDATA=/var/lib/postgresql/data/pgdata \
    -v /custom/mount:/var/lib/postgresql/data \
    postgres


# Run postgresql-exporter

## Start an example database
docker run --net=host -it --rm -e POSTGRES_PASSWORD=password postgres
## Connect to it
docker run --net=host -e DATA_SOURCE_NAME="postgresql://postgres:password@localhost:5432/postgres?sslmode=disable" wrouesnel/postgres_exporter

# Run prometheus

## Volumes & bind-mount
## Bind-mount your prometheus.yml from the host by running:

docker run \
    -p 9090:9090 \
    -v /path/to/prometheus.yml:/etc/prometheus/prometheus.yml \
    prom/prometheus
Or bind-mount the directory containing prometheus.yml onto /etc/prometheus by running:

docker run \
    -p 9090:9090 \
    -v /path/to/config:/etc/prometheus \
    prom/prometheus

# Run grafana

docker run -d \
  -p 3000:3000 \
  --name=grafana \
  -e "GF_INSTALL_PLUGINS=grafana-clock-panel,grafana-simple-json-datasource" \
  grafana/grafana

