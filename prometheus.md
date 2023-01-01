
### add/modify additionalScrapeConfigs

```shell
k get prometheus -n prom prom-stack-kube-prometheus-prometheus -oyaml | yq e '.spec.additionalScrapeConfigs' -
spec:
  additionalScrapeConfigs:
    key: extraScrapeConfigs.yaml
    name: additional-configs


cat extraScrapeConfigs.yaml
- job_name: 'node'
  scrape_interval: 60s
  dns_sd_configs:
    - names:
      - 'arm_exporter'
      type: 'A'
      port: 9243
- job_name: 'hw-node-exporter'
  static_configs:
  - targets: ["10.0.16.76:9100"]
  
k create secret generic additional-configs --from-file=extraScrapeConfigs.yaml --dry-run=client -oyaml -n prom > additional-configs.yaml
  
k apply -f additional-configs.yaml -n prom


k get secret -n prom additional-configs -oyaml | yq e '.data."extraScrapeConfigs.yaml"' - | base64 -d
- job_name: 'node'
  scrape_interval: 60s
  dns_sd_configs:
    - names:
      - 'arm_exporter'
      type: 'A'
      port: 9243
- job_name: 'hw-node-exporter'
  static_configs:
  - targets: ["10.0.16.76:9100"]

```
