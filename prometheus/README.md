# Prometheus Template Example

## Global

The global is uded to define some rules for all the template file.

## prometheus.yml (As a basic template)

```
global:
  scrape_interval:     15s # By default, scrape targets every 15 seconds.
  evaluation_interval: 15s # Evaluate rules every 15 seconds.

  # Attach these extra labels to all timeseries collected by this Prometheus instance.
  external_labels:
    monitor: 'codelab-monitor'

# Not mandatory
rule_files:
- 'prometheus.rules.yml'

scrape_configs:
# The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
- job_name: 'prometheus'

  # Override the global default and scrape targets from this job every 5 seconds.
  scrape_interval: 5s # Overides the global scrape_interval for 'prometheus' jobs

  static_configs:
  - targets: ['localhost:9090']

- job_name: 'node'

  # Override the global default and scrape targets from this job every 5 seconds.
  scrape_interval: 5s

  static_configs:
  - targets: ['localhost:8080', 'localhost:8081']
    labels:
      group: 'production'

  - targets: ['localhost:8082']
    labels:
      group: 'canary'
```

# References

- https://prometheus.io/docs/prometheus/latest/getting_started/