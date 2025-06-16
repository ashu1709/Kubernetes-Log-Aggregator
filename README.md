## Overview

[Fluent Bit](http://fluentbit.io) is a lightweight and flexible **log and metrics processor** designed for Kubernetes. It lets you:

- Gather container and pod logs directly from files or the systemd journal.
- Enrich those logs with additional metadata related to your pods.
- Forward them to a range of backends, including Elasticsearch, Splunk, Datadog, InfluxDB, and more.

This repository includes manifest files (RBAC, Service Accounts, DaemonSet) to aid in deploy Fluent Bit alongside your workloads in a Kubernetes environment.

---

## Installation

Fluent Bit should be deployed as a DaemonSet to enable its functionality across your nodes.

---

### For Kubernetes v1.21 and Below:

```bash
kubectl create namespace logging
kubectl create -f fluent-bit-service-account.yaml
kubectl create -f fluent-bit-role.yaml
kubectl create -f fluent-bit-role-binding.yaml
```

---

### For Kubernetes v1.22 and Above:

```bash
kubectl create namespace logging
kubectl create -f fluent-bit-service-account.yaml
kubectl create -f fluent-bit-role-1.22.yaml
kubectl create -f fluent-bit-role-binding-1.22.yaml
```

---

### If You Are Using OpenShift:

```bash
kubectl create -f fluent-bit-openshift-security-context-constraints.yaml
```

---

## Fluent Bit to Elasticsearch

Create the configuration first:

```bash
kubectl create -f fluent-bit-configmap.yaml
```

Then deploy the DaemonSet:

```bash
kubectl create -f fluent-bit-ds.yaml
```

If you’re testing with Minikube, use:

```bash
kubectl create -f fluent-bit-ds-minikube.yaml
```

---

## Fluent Bit to Kafka

Create the configuration first:

```bash
kubectl create -f fluent-bit-configmap.yaml
```

Then deploy the DaemonSet:

```bash
kubectl create -f fluent-bit-ds.yaml
```

---

## Additional Notes

Fluent Bit’s default configuration:

- Collects all container logs from your nodes.
- Stores up to 5MB of messages before forwarding them.
- Enriches messages with pod metadata.
- Retries delivery until messages are successfully processed.

---
