# sysmon

System monitoring for HSR

## Installation

1. Adapt the [prometheus/prometheus.yml](prometheus/prometheus.yml) file to specify the CTFd IP address in `targets`.
2. Launch containers using docker compose.
3. Connect to grafana on http port `3000`.

```bash
cd sysmon
docker compose up -d
```
