# README / Walkthrough

## Getting started

    $ minikube delete
    $ minikube start --kubernetes-version=v1.8.0 --vm-driver=virtualbox --alsologtostderr
    ...
    Kubectl is now configured to use the cluster.
    Loading cached images from config file.

    $ minikube status
    minikube: Running
    cluster: Running
    kubectl: Correctly Configured: pointing to minikube-vm at 192.168.99.101

    $ kubectl config use-context minikube
    $ kubectl get nodes

## Do something

    $ kubectl run hello-http --image=nginx --port=80
    $ kubectl get pods
    $ kubectl expose deployment hello-http --type=NodePort
    $ kubectl get services
    ...
    $ curl $(minikube service hello-k8s --url)
    $ kubectl scale --replicas=3 deployment/hello-http
    $ kubectl get deployment
    $ kubectl get pods

## Do the same with YAML

    $ kubectl create -f hello.yml

## Good to know

 - Pods are a model of the pattern of multiple cooperating processes which form a cohesive unit of service. They simplify application deployment and management by providing a higher-level abstraction than the set of their constituent applications.
 - A Deployment is a higher-level concept that manages ReplicaSets and provides declarative updates to pods along with a lot of other useful features. Therefore, it is recommended to use Deployments instead of directly using ReplicaSets.

## References

 - [Hello Minikube Tutorial](https://kubernetes.io/docs/tutorials/stateless-application/hello-minikube/#create-a-docker-container-image)
 - [Romin Irani's Tutorial](https://rominirani.com/tutorial-getting-started-with-kubernetes-on-your-windows-laptop-with-minikube-3269b54a226)
 - [Jenkins on K8s](https://www.blazemeter.com/blog/how-to-setup-scalable-jenkins-on-top-of-a-kubernetes-cluster)
 