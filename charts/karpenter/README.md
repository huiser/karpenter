# karpenter

A Helm chart for https://github.com/aws/karpenter/.

![Version: 0.5.3](https://img.shields.io/badge/Version-0.5.3-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)

## Installing the Chart

To install the chart with the release name `karpenter`:

```console
$ helm repo add karpenter https://charts.karpenter.sh
$ helm repo update
$ helm upgrade --install karpenter karpenter/karpenter --namespace karpenter \
  --create-namespace --set serviceAccount.create=false --version 0.5.3 \
  --set controller.clusterName=${CLUSTER_NAME} \
  --set controller.clusterEndpoint=$(aws eks describe-cluster --name ${CLUSTER_NAME} --query "cluster.endpoint" --output json) \
  --wait # for the defaulting webhook to install before creating a Provisioner 
```

You can follow the detailed installation instruction [here](https://karpenter.sh/docs/getting-started/#install).

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| controller.affinity | object | `{}` | Affinity rules for scheduling |
| controller.clusterEndpoint | string | `""` | Cluster endpoint |
| controller.clusterName | string | `""` | Cluster name |
| controller.env | list | `[]` | Additional environment variables to run with |
| controller.image | string | `"public.ecr.aws/karpenter/controller:v0.5.3@sha256:ddd24d756cb324cf8f91f2274621646f83d6121ed6856312ca672a5f78c57174"` | Image to use for the Karpenter controller |
| controller.nodeSelector | object | `{}` | Node selectors to schedule to nodes with labels. |
| controller.replicas | int | `1` |  |
| controller.resources.limits.cpu | int | `1` |  |
| controller.resources.limits.memory | string | `"1Gi"` |  |
| controller.resources.requests.cpu | int | `1` |  |
| controller.resources.requests.memory | string | `"1Gi"` |  |
| controller.tolerations | list | `[]` | Tolerations to schedule to nodes with taints. |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account (like the ARN of the IRSA role) |
| serviceAccount.create | bool | `true` | Create a service account for the application controller |
| serviceAccount.name | string | `"karpenter"` | Service account name |
| webhook.affinity | object | `{}` | Affinity rules for scheduling |
| webhook.env | list | `[]` | List of environment items to add to the webhook |
| webhook.hostNetwork | bool | `false` | Set to true if using custom CNI on EKS |
| webhook.image | string | `"public.ecr.aws/karpenter/webhook:v0.5.3@sha256:19a1e1f2c8ec6ece1b170584dd6251d2e00f1676503a65d1433f45f46e330ddf"` | Image to use for the webhook |
| webhook.nodeSelector | object | `{}` | Node selectors to schedule to nodes with labels. |
| webhook.port | int | `8443` |  |
| webhook.replicas | int | `1` |  |
| webhook.resources.limits.cpu | string | `"100m"` |  |
| webhook.resources.limits.memory | string | `"50Mi"` |  |
| webhook.resources.requests.cpu | string | `"100m"` |  |
| webhook.resources.requests.memory | string | `"50Mi"` |  |
| webhook.tolerations | list | `[]` | Tolerations to schedule to nodes with taints. |

