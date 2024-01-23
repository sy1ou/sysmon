# sysmon

System monitoring for HSR

## Nginx exporter config

Expose the built-in metrics in NGINX

```txt
  server {
    listen 8080;
    location = /stub_status {
      stub_status;
    }
  }
```

Run the exporter in the Docker Compose

```yaml
  nginx-exporter:
    image: nginx/nginx-prometheus-exporter:1.1.0
    restart: always
    ports:
      - 9113:9113
    depends_on:
      - nginx
    command:
      - "--nginx.scrape-uri=http://nginx:8080/stub_status"
```

## CTFd exporter config

Create a `.env` file and fill out the appropriate values.

```txt
# API key for the CTFd instance
CTFD_API=<key>

# URL of the CTFd instance
CTFD_URL=<url>

# The polling rate of the exporter in seconds
POLL_RATE=<seconds>
```

Run the exporter in the Docker Compose

```yaml
  ctfd-exporter:
    image: ghcr.io/eliabir/ctfd-exporter:latest
    environment:
      CTFD_API: ${CTFD_API}
      CTFD_URL: ${CTFD_URL}
      POLL_RATE: ${POLL_RATE}
    ports:
      - 2112:2112
    restart: unless-stopped
```

