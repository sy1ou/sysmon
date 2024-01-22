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

