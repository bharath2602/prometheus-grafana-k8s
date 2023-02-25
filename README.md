# Prometheus-Grafana Manifests


## Getting started

```
git clone https://github.com/bharath2602/prometheus-grafana-k8s.git
cd existing_repo
git remote add origin https://github.com/bharath2602/prometheus-grafana-k8s.git
git branch -M main
git push -uf origin main
```

## Notable Points

- Create a new name space for the monitring applications and apply all the manifest to that name space using **-n** parameter to the kubectl commands 
- All the monitoring tools are made run as pods in the K8s cluster
- Both the prometheus and grafana needs a configuration file
- All the application needed to be monitored need to expose metrics in '/metric' path any custome path needs to be mentioned in the service annotations

    ```
    prometheus.io/path: "/actuator/prometheus" --> path exposing the metrics
    prometheus.io/port: "8080" --> port exposed in the service
    prometheus.io/scrape: "true" --> for auto-discovery of the service by prometheus
    ```

- Refernce:

    - [Prometheus](https://devopscube.com/setup-prometheus-monitoring-on-kubernetes/)
    - [State-metric](https://devopscube.com/setup-kube-state-metrics/)
    - [Grafana](https://devopscube.com/setup-grafana-kubernetes/)


![alt text](https://github.com/bharath2602/prometheus-grafana-k8s/blob/main/Outputs/Screenshot%202023-02-25%20at%203.15.35%20PM.png?raw=true)
