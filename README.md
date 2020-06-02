# simple-prometheus-installation

1. Run `kubectl apply -f prometheus.yaml`

1. Add annotations to deployments that you like to have Prometheus collect. Replace the port (`8080`) and path (`/metrics`) with the correct ones that your pod exposes.
<pre><tt>apiVersion: apps/v1
kind: Deployment

metadata:
  name: web
  labels:
    comp: web

spec:
  replicas: 1
  revisionHistoryLimit: 2
  selector:
    matchLabels:
      comp: web
  template:
    metadata:
      labels:
        comp: web
      annotations: <strong>
        prometheus.io/path: /metrics
        prometheus.io/port: '8080'
        prometheus.io/scrape: 'true'</strong>
    spec:
      containers:
      ...</tt></pre>
3. If your app is not configured to expose metrics to Prometheus, add the envoy_container.yaml container definition to the containers of the application you are seeking to optimize, replacing the SERVICE_PORT env var with the service port your application exposes
