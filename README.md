# Kubeflow Image Loader Using Shell Script

This repo is for to pull/push docker image to registry based on Kubeflow.

## Usage

**Preperation**:  
Before Using Loader, Docker must be pre-installed. And Image capacity takes about 30G. Look at Image list needed for Kubeflow installation *(version: 0.7.1)*

```
argoproj/argoui:v2.3.0
argoproj/workflow-controller:v2.3.0
docker.io/istio/citadel:1.1.6
docker.io/istio/galley:1.1.6
docker.io/istio/kubectl:1.1.6
docker.io/istio/mixer:1.1.6
docker.io/istio/pilot:1.1.6
docker.io/istio/proxy_init:1.1.6
docker.io/istio/proxyv2:1.1.6
docker.io/istio/sidecar_injector:1.1.6
docker.io/jaegertracing/all-in-one:1.9
docker.io/kiali/kiali:v0.16
docker.io/prom/prometheus:v2.3.1
docker.io/seldonio/seldon-core-operator:0.4.1
gcr.io/google_containers/spartakus-amd64:v1.1.0
gcr.io/kfserving/alibi-explainer:0.2.2
gcr.io/kfserving/kfserving-controller:0.2.2
gcr.io/kfserving/logger:0.2.2
gcr.io/kfserving/pytorchserver:0.2.2
gcr.io/kfserving/sklearnserver:0.2.2
gcr.io/kfserving/storage-initializer:0.2.2 
gcr.io/kfserving/xgbserver:0.2.2
gcr.io/kubebuilder/kube-rbac-proxy:v0.4.0
gcr.io/kubeflow-images-public/admission-webhook:v20190520-v0-139-gcee39dbc-dirty-0d8f4c
gcr.io/kubeflow-images-public/ingress-setup:latest
gcr.io/kubeflow-images-public/jupyter-web-app:9419d4d
gcr.io/kubeflow-images-public/katib/v1alpha3/katib-controller:v0.7.0
gcr.io/kubeflow-images-public/katib/v1alpha3/katib-manager:v0.7.0
gcr.io/kubeflow-images-public/katib/v1alpha3/katib-ui:v0.7.0
gcr.io/kubeflow-images-public/kubernetes-sigs/application:1.0-beta
gcr.io/kubeflow-images-public/metadata-frontend:v0.1.8
gcr.io/kubeflow-images-public/metadata:v0.1.11
gcr.io/kubeflow-images-public/pytorch-operator:v0.7.0
gcr.io/kubeflow-images-public/tensorflow-1.14.0-notebook-cpu:v-base-ef41372-1177829795472347138
gcr.io/kubeflow-images-public/tensorflow-1.14.0-notebook-cpu:v0.7.0
gcr.io/kubeflow-images-public/tensorflow-1.14.0-notebook-gpu:v0.7.0
gcr.io/kubeflow-images-public/tensorflow-2.0.0a0-notebook-cpu:v0.7.0
gcr.io/kubeflow-images-public/tensorflow-2.0.0a0-notebook-gpu:v0.7.0
gcr.io/kubeflow-images-public/tf_operator:kubeflow-tf-operator-postsubmit-v1-5adee6f-6109-a25c
gcr.io/ml-pipeline/api-server:0.1.31
gcr.io/ml-pipeline/envoy:metadata-grpc
gcr.io/ml-pipeline/frontend:0.1.31
gcr.io/ml-pipeline/persistenceagent:0.1.31
gcr.io/ml-pipeline/scheduledworkflow:0.1.31
gcr.io/ml-pipeline/viewer-crd-controller:0.1.31
gcr.io/ml-pipeline/visualization-server:0.1.27
gcr.io/tfx-oss-public/ml_metadata_store_server:0.15.1
grafana/grafana:6.0.2
mcr.microsoft.com/onnxruntime/server:v0.5.1
metacontroller/metacontroller:v0.3.0
minio/minio:RELEASE.2018-02-09T22-40-05Z
mysql:5.6
mysql:8
mysql:8.0.3
nvcr.io/nvidia/tensorrtserver:19.05-py3
tensorflow/serving:1.11.0
tensorflow/serving:1.11.0-gpu
tensorflow/serving:1.12.0
tensorflow/serving:1.12.0-gpu
tensorflow/serving:1.13.0
tensorflow/serving:1.13.0-gpu
tensorflow/serving:1.14.0
tensorflow/serving:1.14.0-gpu
tensorflow/tensorflow:1.8.0
gcr.io/knative-releases/knative.dev/serving/cmd/activator@sha256:88d864eb3c47881cf7ac058479d1c735cc3cf4f07a11aad0621cd36dcd9ae3c6
gcr.io/knative-releases/knative.dev/serving/cmd/autoscaler-hpa@sha256:a7801c3cf4edecfa51b7bd2068f97941f6714f7922cb4806245377c2b336b723
gcr.io/knative-releases/knative.dev/serving/cmd/autoscaler@sha256:aeaacec4feedee309293ac21da13e71a05a2ad84b1d5fcc01ffecfa6cfbb2870
gcr.io/knative-releases/knative.dev/serving/cmd/controller@sha256:3b096e55fa907cff53d37dadc5d20c29cea9bb18ed9e921a588fee17beb937df
gcr.io/knative-releases/knative.dev/serving/cmd/networking/istio@sha256:057c999bccfe32e9889616b571dc8d389c742ff66f0b5516bad651f05459b7bc
gcr.io/knative-releases/knative.dev/serving/cmd/queue@sha256:e0654305370cf3bbbd0f56f97789c92cf5215f752b70902eba5d5fc0e88c5aca
gcr.io/knative-releases/knative.dev/serving/cmd/webhook@sha256:c2076674618933df53e90cf9ddd17f5ddbad513b8c95e955e45e37be7ca9e0e8
gcr.io/kubeflow-images-public/centraldashboard@sha256:4299297b8390599854aa8f77e9eb717db684b32ca9a94a0ab0e73f3f73e5d8b5
gcr.io/kubeflow-images-public/kfam@sha256:3b0d4be7e59a3fa5ed1d80dccc832312caa94f3b2d36682524d3afc4e45164f0
gcr.io/kubeflow-images-public/notebook-controller@sha256:6490f737000bd1d2520ac4b8cbde2b09749cdb291b1967ddda95d05131db49db
gcr.io/kubeflow-images-public/profile-controller@sha256:e601b2226e534a4f8e0722cfc44ae4a919a90265c4c6c9e7a7a55fcb57032f25
```

**help**:  
Let's look at the script. For example:  
```bash
$ ./imageLoader
usage:
    ./imageLoader pull
    ./imageLoader push
```

### pull

Use the pull option to convert the image needed for kubeflow installation into a tar file. At this time, the tar file is created in the `tars /` folder and occupies about 30G. `.imageList` and` .imageListHash` contain lists with or without image tags.

### push

The push option pushes the image tar file in the `tars` folder to a specific docker registry. Before execution, the address must be added to the `registry` variable in the imageLoader script. For example:  
```bash
#!/bin/bash
# Fri, 18.05.2020
# jaejun.lee.1991@gmail.com

registry={registry_ip}:{registry_port}

...
...
```

---

made by *jaejun.lee*
