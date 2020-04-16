# simple-prometheus-installation

1. Run `kubectl apply -f prometheus.yaml`
1. If your app is not configured to expose metrics to prometheus, add the envoy_container.yaml container definition to the containers of the application you are seeking to optimize, replacing the SERVICE_PORT env var with the service port your application exposes
