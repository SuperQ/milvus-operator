# Milvus Operator

[![CI Pipeline](https://github.com/zilliztech/milvus-operator/actions/workflows/ci.yml/badge.svg)](https://github.com/zilliztech/milvus-operator/actions/workflows/ci.yml/badge.svg)
[![codecov](https://codecov.io/gh/zilliztech/milvus-operator/branch/main/graph/badge.svg?token=DAXmgusBQq)](https://codecov.io/gh/zilliztech/milvus-operator)
[![Go Reference](https://pkg.go.dev/badge/github.com/zilliztech/milvus-operator.svg)](https://pkg.go.dev/github.com/zilliztech/milvus-operator)
<img src="https://img.shields.io/github/license/milvus-io/milvus" alt="license">


> **ATTENTIONS:** THE `MAIN` BRANCH MAY BE IN AN UNSTABLE OR EVEN BROKEN STATE DURING DEVELOPMENT.

## Overview
[Milvus](https://milvus.io) is a cloud-native, open-source vector database built to manage embedding vectors generated by machine learning models and neural networks. It extends the capabilities of best-in-class approximate nearest neighbor (ANN) search libraries (e.g. Faiss, NMSLIB, Annoy) and features on-demand scalability, and high availability.

The Milvus Operator provides an easy and solid solution to deploy and manage a full Milvus service stack including both the milvus components and its relevant dependencies such as etcd, pulsar and minio to the target [Kubernetes](https://kubernetes.io/) clusters in a scalable and high-available way. The Milvus Operator defines a milvuscluster custom resources on top of Kubernetes [Custom Resources](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/). The Kubernetes API can then be used in a declarative way to manage Milvus deployment stack and ensure its scalability and high-availability operation.

# Getting started
## Deploy milvus operator

Install or upgrade to latest version with helm:

```shell
helm repo add milvus-operator https://zilliztech.github.io/milvus-operator/
helm repo update milvus-operator
helm -n milvus-operator upgrade --install --create-namespace milvus-operator milvus-operator/milvus-operator
```

Or with kubectl & raw manifests:

```shell
kubectl apply -f https://raw.githubusercontent.com/zilliztech/milvus-operator/v0.8.8/deploy/manifests/deployment.yaml
```

For more infomation Check [Installation Instructions](docs/installation/installation.md)

## Create milvus demo instance
```shell
kubectl apply -f https://raw.githubusercontent.com/zilliztech/milvus-operator/main/config/samples/demo.yaml
```

> Note: The demo instance starts a standalone milvus & its dependencies with the least resources requests. It is not suitable for production environment. For more deployment examples please check https://github.com/zilliztech/milvus-operator/blob/main/config/samples

# Versioning

Versions of the underlying components are listed below:

<!-- source csv for table
Components, Milvus, Pulsar / Kafka, Etcd, MinIO
Versions, v2.3.5 `[1]`, 2.8.2 / 3.1.0, 3.5.5-2, RELEASE.2023-03-20T20-16-18Z -->

|Components| Milvus| Pulsar / Kafka| Etcd| MinIO|
|---|---|---|---|---|
|Versions| v2.3.5 `[1]`| 2.8.2 / 3.1.0 | 3.5.5-2 |RELEASE.2023-03-20T20-16-18Z|


> `[1]` Version of milvus is the default version we will use, you can set it to other version. The Compatibility with milvus releases is showed below.

## Compatibility With Milvus Releases

<!-- source csv for table
Milvus Versions, <=v2.0.0-rc8, v2.0.0-pre-ga, >=v2.0.0
Compatibility, ✖️, ✔️, ✔️  -->

|Milvus Versions| <=v2.0.0-rc8| v2.0.0-pre-ga| >=v2.0.0|
|---|---|---|---|
|Compatibility| ✖️| ✔️| ✔️|

## Compatibility With Milvus-Operator Earlier Releases

<!-- source csv for table
Milvus Operator Versions, <0.4.0, >=0.4.0
Compatibility, ✖️, ✔️  -->

|Milvus Operator Versions| <0.4.0| >=0.4.0|
|---|---|---|
|Compatibility| ✖️| ✔️|


# Install / upgrade milvus-operator of a specific version

Use helm:

```shell
helm upgrade --install milvus-operator \
  -n milvus-operator --create-namespace \
  https://github.com/zilliztech/milvus-operator/releases/download/v0.8.8/milvus-operator-0.8.8.tgz
```

Or use kubectl & raw manifests:

```shell
kubectl apply -f https://raw.githubusercontent.com/zilliztech/milvus-operator/v0.8.8/deploy/manifests/deployment.yaml
```


# Documentations
- [Installation](docs/installation/installation.md)
- [Install KinD for development](docs/installation/kind-installation.md)
- Administration Guides:
  - [Configure Milvus with Milvus Operator](docs/administration/configure-milvus.md)
  - Manage Dependencies:
    - [Configure Meta Storge](docs/administration/manage-dependencies/meta-storage.md)
    - [Configure Object Storage](docs/administration/manage-dependencies/object-storage.md)
    - [Configure Message Storage](docs/administration/manage-dependencies/message-storage.md)
  - [Monitor And Alert](docs/administration/monitor-and-alert.md)
  - [Allocate Resources](docs/administration/allocate-resources.md)
  - [Scale A Milvus Cluster](docs/administration/scale-a-milvus-cluster.md)
  - [Upgrade](docs/administration/upgrade.md)
  - Security:
    - [Enable TLS](docs/administration/security/encryption-in-transit.md)
    - [Enable Authentication](docs/administration/security/enable-authentication.md)
- [Milvus CRD Reference](docs/CRD/milvus.md)
- [How it works](docs/arch/arch.md)
