# Deploying Jenkins

## Deploying with the YAML

Based on [this simple guide](https://www.blazemeter.com/blog/how-to-setup-scalable-jenkins-on-top-of-a-kubernetes-cluster) written by Yuri Bushnev. It's easier to deploy through Helm.

## Deploying with Helm

Based on [this Prometheus + Jenkins](https://github.com/javajon/jenkins-kubernetes) deployment by Jonathan Johnson, partially. The steps are as followed:

```bash
$ helm init
$ helm repo update
$ helm repo list
$ helm repo add coreos https://s3-eu-west-1.amazonaws.com/coreos-charts/stable/
$ helm install coreos/prometheus-operator --wait --name prometheus-operator --namespace monitoring
$ helm install coreos/kube-prometheus --wait --name kube-prometheus --namespace monitoring
$ helm install stable/jenkins --namespace jenkins --name jenkins -f ./jenkins-values.yaml
$ kubectl create -f rbac.yml
$ kubectl get deployments,pods -n jenkins
$ kubectl get services -n jenkins
```

**Note:** Do not turn RBAC off with `--set rbacEnable=false` during `helm install`. You will likely run into container initilization error (mounting and secret related).

## Accessing Grafana

The deployment earlier jas installed Prometheus to the cluster. In order to access it (via Grafana), you will need to [set up a Load Balancer](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/) (see also [Exposing an external IP](https://kubernetes.io/docs/tutorials/stateless-application/expose-external-ip-address/)) or to patch `spec/type` to `NodePort`:

```bash
$ kubectl patch service kube-prometheus-grafana --namespace=monitoring --type='json' -p='[{"op": "replace",  "path": "/spec/type", "value":"NodePort"}]'
```

## References

 - [More about Prometheus operator -- workflow and deployment](https://akomljen.com/get-kubernetes-cluster-metrics-with-prometheus-in-5-minutes/)
 - [prometheus-operator's issue #1368 on RBAC](https://github.com/coreos/prometheus-operator/issues/1368)
