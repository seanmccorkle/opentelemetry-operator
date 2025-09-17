# opentelemetry-operator

[OpenTelemetry Operator](https://github.com/open-telemetry/opentelemetry-operator)<br>
[github.com: Target Allocator](https://github.com/open-telemetry/opentelemetry-operator/blob/main/cmd/otel-allocator/README.md)<br>
[openTelemetry.io: Target Allocator](https://opentelemetry.io/docs/kubernetes/operator/target-allocator/)<br>
[Target allocator not picking up Prometheus ServiceMonitor](https://github.com/open-telemetry/opentelemetry-operator/issues/1851)<br>
[Opentelemetry target allocator does not allocate discovered ServiceMonitors](https://stackoverflow.com/questions/77269471/opentelemetry-target-allocator-does-not-allocate-discovered-servicemonitors)<br>
[Let’s Learn About the OTel Operator’s Target Allocator!](https://adri-v.medium.com/lets-learn-about-the-otel-operator-s-target-allocator-47a2b1f07562)<br>
[Prometheus Receiver](https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/receiver/prometheusreceiver/README.md)<br>
[otc-container sidecar container is restarted infinitely if istio injection is enabled](https://github.com/open-telemetry/opentelemetry-operator/issues/946)<br>
[Sidecar injection fails when Operator ready after target Pods](https://github.com/open-telemetry/opentelemetry-operator/issues/1765)<br>
[opentelemetry-operator sidecar injection failing](https://github.com/open-telemetry/opentelemetry-operator/issues/1898)<br>
[Is there a way to provide the config in Instrumentation and OpenTelemetryCollector in the form of a configmap?](https://github.com/open-telemetry/opentelemetry-operator/issues/1196)<br>
[TargetAllocator : error during loading configuration](https://github.com/open-telemetry/opentelemetry-operator/issues/1811)<br>
[Target Allocator not able to allocate](https://github.com/open-telemetry/opentelemetry-collector-contrib/issues/23342)<br>
[opentelemetry.io: getting started](https://opentelemetry.io/docs/kubernetes/getting-started/)<br>
[Target Allocator - ServiceMonitor scheme](https://github.com/open-telemetry/opentelemetry-operator/issues/1669)<br>
[Things You Might Not Have Known About the OpenTelemetry Operator](https://geekingoutpodcast.substack.com/p/otel-operator-q-and-a)<br>

# install

[cert-manager installation](https://cert-manager.io/docs/installation/)<br>
[installing cert-manager](https://cert-manager.io/docs/installation/helm/#installing-cert-manager)<br>
```
helm repo add jetstack https://charts.jetstack.io --force-update
helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version v1.14.3 --set crds.enabled=true
```

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus-crds prometheus-community/prometheus-operator-crds
helm install prometheus prometheus-community/prometheus (optional)
```

[docker pull opentelemetry-operator](https://github.com/open-telemetry/opentelemetry-operator/pkgs/container/opentelemetry-operator%2Fopentelemetry-operator)<br>
```
docker pull ghcr.io/open-telemetry/opentelemetry-operator/opentelemetry-operator:main
helm repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts
helm repo update
kubectl create namespace opentelemetry-operator-system

helm install opentelemetry-operator ../opentelemetry-operator --namespace opentelemetry-operator-system --set admissionWebhooks.certManager.enabled=false --set admissionWebhooks.autoGenerateCert.enabled=true

helm install opentelemetry-operator open-telemetry/opentelemetry-operator -f values.yaml -n opentelemetry-operator-system

kubectl --namespace opentelemetry-operator-system get pods -l "app.kubernetes.io/instance=opentelemetry-operator"
```

# images

```
.Values.manager.image = ghcr.io/open-telemetry/opentelemetry-operator/opentelemetry-operator:main
.Values.manager.collectorImage = otel/opentelemetry-collector
.Values.manager.collectorImage = otel/opentelemetry-collector-contrib
.Values.manager.targetAllocatorImage = ghcr.io/open-telemetry/opentelemetry-operator/target-allocator:main

```

# troubleshooting

[Troubleshooting the OpenTelemetry Target Allocator](https://trstringer.com/opentelemetry-target-allocator-troubleshooting/)<br>
```
kubectl port-forward service/otel-collector-ta-targetallocator 8080:80 -n opentelemetry-operator-system
curl localhost:8080/jobs | jq
curl localhost:8080/jobs/otel-collector-self-metrics/targets | jq
curl localhost:8080/scrape_configs | jq
```
