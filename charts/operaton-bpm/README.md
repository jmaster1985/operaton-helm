# Operaton BPM Helm Chart

## How to install
todo: add repo, install chart

## Security
The default security settings for the container are configured under `securityContext` in `values.yaml`. 
These settings are appropriate for using Operaton with an H2 database. For production use, 
where an external database is used, consider enabling the setting `readOnlyRootFilesystem: true` 
to ensure that the root file system of your container remains read-only.

## Performance and Resource Consumption
The configuration related to resource consumption (CPU and memory) can be found under `resources` in `values.yaml`. 
The default settings allocate a minimum of 250 milli-CPU cores and 512Mi of memory, with a maximum limit of 1 CPU core 
and 1Gi of memory per pod. This ensures fair resource usage within your cluster and prevents 
a single pod from exhausting available resources.
With these settings, a new pod typically starts in around 20 seconds. If your cluster allows 
for higher resource allocation, consider increasing the values under `limits` to enhance performance.

## Autoscaling
By default, autoscaling is disabled for this chart. However, it is highly recommended to enable 
it for production use. The autoscaling settings can be found under `autoscaling` in `values.yaml`.
The current configuration scales up by adding a new instance when the average CPU usage 
across existing instances exceeds 80%. Please note that autoscaling requires a minimum amount 
of resources per pod, which can be defined under `resources.requests`.