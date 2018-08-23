# `stackstorm-enterprise-ha` Helm Chart
StackStorm Enterprise K8s Helm Chart, optimized for running StackStorm in HA environment.

It will install 2 replicas for each component of StackStorm microservices for redundancy, as well as backends like
RabbitMQ HA, MongoDB replicaset and etcd cluster that st2 replies on for MQ, DB and distributed coordination respectively.

It's more than welcome to configure each component in-depth to fit specific availability/scalability demands.

## Usage
1) Edit `values.yaml` with configuration for the StackStorm Enterprise HA K8s cluster.
> NB! It's highly recommended to set your own secrets as file contains unsafe defaults like self-signed SSL certificates, SSH keys,
> StackStorm access and DB/MQ passwords!

2) Pull 3rd party Helm dependencies:
```
helm dependency update
```

3) Install the chart:
```
helm install .
```

4) Upgrade.
Once you made any changes in values, to upgrade the cluster:
```
helm upgrade <release-name> .
```

## Components
### st2web
By default, st2web includes a Pod Deployment and a Service for st2web Enterprise Web UI.
Service uses NodePort, so installing this chart will not provision a LoadBalancer or Ingress (TODO!).
Depending on your Kubernetes cluster configuration you may need to add additional configuration to access the example service.
