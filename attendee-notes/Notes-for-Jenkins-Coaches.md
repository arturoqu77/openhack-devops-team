# Overview

The goal of this guide is to help coaches with their Jenkins-based teams to overcome common challenges unique to Jenkins and related OSS stack (i.e. Prometheus/Grafana).  General challenge information in the "Notes for Coaches" should be consulted first  since this information is still largely applicable to Jenkins teams.

## Challenge 6

This walks through how to accomplish the challenge using Prometheus and Grafana running on top of AKS.

### Install Prometheus

helm install --name prom --namespace monitor stable/prometheus --set alertmanager.persistentVolume.storageClass="managed-premium",server.persistentVolume.storageClass="managed-premium"

### Install Grafana

helm install --name grafana --namespace=monitor stable/grafana -f grafana-values.yml

grafana-values.yml

```yaml
persistence:
  enabled: true
  storageClassName: managed-premium
  accessModes:
    - ReadWriteOnce
  size: 10Gi
datasources:
 datasources.yaml:
   apiVersion: 1
   datasources:
   - name: Prometheus
     type: prometheus
     url: http://prom-prometheus-server
     access: proxy
     isDefault: true
plugins: [grafana-azure-monitor-datasource]
```

Connect to the grafana instance:

`kubectl --namespace monitor port-forward svc/grafana 3000:80`

### Configure Grafana Dashboard

Quick dashboard to import and show something for K8s info:
<https://grafana.com/dashboards/315>

After configuring the Azure Monitor Data source, people could easily add the required SQL statistics to the above example dashboard.

The API response times will require more work.  Options include:

- Istio mesh info (if teams go that route)
- Wire APIs for telemetry
    - App Insights --> Surface via Azure Monitor
    - Prometheus --> Custom query
- Enable OMS logging on the cluster and then gather this data via a query with the Azure Monitor grafana plugin
