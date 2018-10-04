# Deploying Jenkins

## Deploying with the YAML

Based on [this simple guide](https://www.blazemeter.com/blog/how-to-setup-scalable-jenkins-on-top-of-a-kubernetes-cluster) written by Yuri Bushnev. It's easier to deploy through Helm.

## Deploying with Helm

Based on [this Prometheus + Jenkins](https://github.com/javajon/jenkins-kubernetes) deployment by Jonathan Johnson, partially. Steps:

```bash
$ helm init
$ helm repo update
$ helm install coreos/kube-prometheus --wait --name kube-prometheus --namespace monitoring --set global.rbacEnable=false
$ helm install stable/jenkins --namespace jenkins --name jenkins -f ./jenkins-values.yaml
$ kubectl create -f rbac.yml
$ kubectl get deployments,pods -n jenkins
```
