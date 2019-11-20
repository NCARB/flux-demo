# EKS
https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html


```sh
eksctl create cluster \
--name eks-demo-01 \
--version 1.14 \
--nodegroup-name standard-workers \
--node-type t3.medium \
--nodes 3 \
--nodes-min 1 \
--nodes-max 4 \
--node-ami auto
```

# windows

https://docs.aws.amazon.com/eks/latest/userguide/windows-support.html


```sh
eksctl utils install-vpc-controllers --name eks-demo-01 --approve
```

```
eksctl create nodegroup \
--region us-west-2 \
--cluster eks-demo-01 \
--name windows-ng \
--node-type t2.large \
--nodes 2 \
--nodes-min 1 \
--nodes-max 2 \
--node-ami-family WindowsServer2019FullContainer
```

# flux

https://docs.fluxcd.io/en/latest/tutorials/get-started.html

```sh
kubectl create ns flux
```

```sh
export GHUSER="feinoujc"

fluxctl install \
--git-user=${GHUSER} \
--git-email=${GHUSER}@users.noreply.github.com \
--git-url=git@github.com:${GHUSER}/flux-demo \
--git-path=namespaces,services \
--namespace=flux | kubectl apply -f -
```


# nginx

https://aws.amazon.com/blogs/opensource/network-load-balancer-nginx-ingress-controller-eks/

# fluentd

https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Container-Insights-setup-logs.html

Needed to attch `CloudWatchAgentServerPolicy` (see https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Container-Insights-prerequisites.html) to node role


```
kubectl create configmap cluster-info \
--from-literal=cluster.name=eks-demo-01 \
--from-literal=logs.region=us-west-2 -n amazon-cloudwatch -o yaml --dry-run > services/amazon-cloudwatch/configmap.yaml
```

