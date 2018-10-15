# README / Walkthrough

## First Time!

    $ minikube delete
    $ minikube start --alsologtostderr
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

Like, [running an example job](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/#running-an-example-job):

    $ kubectl create -f https://k8s.io/examples/controllers/job.yaml

Or [running Nginx](https://kubernetes.io/docs/reference/kubectl/docker-cli-to-kubectl/#docker-run):

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

## Do more: Deploy Jenkins

See [`jenkins/README.md`](jenkins/README.md).

## Good to know

 - Pods are a model of the pattern of multiple cooperating processes which form a cohesive unit of service. They simplify application deployment and management by providing a higher-level abstraction than the set of their constituent applications.
 - A Deployment is a higher-level concept that manages ReplicaSets and provides declarative updates to pods along with a lot of other useful features. Therefore, it is recommended to use Deployments instead of directly using ReplicaSets.

## References

 - [Hello Minikube Tutorial](https://kubernetes.io/docs/tutorials/stateless-application/hello-minikube/#create-a-docker-container-image)
 - [Romin Irani's Tutorial](https://rominirani.com/tutorial-getting-started-with-kubernetes-on-your-windows-laptop-with-minikube-3269b54a226)
 - [Bitnami: Deploy, scale and upgrade with Helm](https://docs.bitnami.com/kubernetes/how-to/deploy-application-kubernetes-helm/)
 - [](https://kubernetes.io/blog/2018/04/30/zero-downtime-deployment-kubernetes-jenkins/)
 - [](https://www.digitalocean.com/community/tutorials/modernizing-applications-for-kubernetes)
