## Overview

<h4>
Basic concepts of kubernets: Node, Pods, Deployments, Services, Storage, Configmap and Secret
</h4>

## Install Docker in AWS (Amazon linux)

```
1. sudo yum update -y (update latest soft)
2. sudo yum install -y docker
3. sudo service docker start
```

## Install Docker Compose in AWS (Amazon linux)

```
1. sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
2. sudo chmod 666 /var/run/docker.sock
3. sudo chmod +x /usr/local/bin/docker-compose;
```

## Install k8s (Amazon linux)

```
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
```

## Get started kubernetes commands

<h6>Check kubernetes version</h6>

```
kubectl version
```

<h6>View cluster info</h6>

```
kubectl cluster-info
```

<h6>Get information about kubernetes Pods, Deployments, Service ...</h6>

```
kubectl get all
```

<h6>Create a resource (resource mean pod, deployment, service)</h6>

```
kubectl create [resource]
```

<h6>Create or modify a resource (resource mean pod, deployment, service)</h6>

```
kubectl apply [resource]
```

<h6>Delete resource</h6>

```
kubectl delete [resource-name]
```

<h6>Forward a port to allow external access</h6>

```
kubectl port-forward [name-of-pod] [external-port]:[internal-port]
```

## Node

https://kubernetes.io/docs/concepts/architecture/nodes/

https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/explore-intro/

A Node is a worker machine in Kubernetes and may be either a virtual or a physical machine, depending on the cluster. Each Node is managed by the control plane. A Node can have one or multiple pods

## Pods

https://kubernetes.io/docs/concepts/workloads/pods/

Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

A Pod (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers.

<h6>List Pods</h6>

```
kubectl get pods
```

<h6>Create Pod</h6>

```
kubectl create -f [pod-file-name].yml eg: kubectl create -f nginx.pod.yml
```

<h6>Create or modify Pod</h6>

```
kubectl apply -f [pod-file-name].yml eg: kubectl apply -f nginx.pod.yml
```

<h6>Delete Pod</h6>

```
kubectl delete pod [name-of-pod] eg: kubectl delete pod my-nginx
```

<h6>Get information of Pod</h6>

```
kubectl describe pod [pod-name] eg: kubectl describe pod my-nginx
```

<h6>Go to bash shell</h6>

```
kubectl exec -it [pod-name] sh eg: kubectl exec -it my-nginx sh
```

## Deployments

https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

Pod can be created and destroyed but can not re-created. So what happend if a Pod is destroyed?
Deployment and replicasets make sure Pods stay running and can be use to scale Pods
No need create Pod directly. We can use Deployment instead of Pod.
A Deployment manages Pods

- Pods are managed using replicasets
- Scale replicasets will be scale Pods
- Zero downtime

<h6>List Deployments</h6>

```
kubectl get deployments
```

<h6>List Deployments and their labels</h6>

```
kubectl get deployments --show-labels
```

<h6>Create Deployment</h6>

```
kubectl create -f [deployment-file-name].yml eg: kubectl create -f nginx.deployment.yml
```

<h6>Create or modify Deployment</h6>

```
kubectl apply -f [deployment-file-name].yml eg: kubectl apply -f nginx.deployment.yml
```

<h6>Delete Deployment</h6>

```
kubectl delete deployment [name-of-deployment] eg: kubectl delete deployment my-nginx
```

<h6>Get information of Deployment</h6>

```
kubectl describe deployment [deployment-name] eg: kubectl describe deployment my-nginx
```

<h6>Get rollout status of Deployment</h6>

```
kubectl rollout status deployment [deployment-name] eg: kubectl rollout status deployment my-nginx
```

<h6>Get history of Deployment</h6>

```
kubectl rollout history deployment [deployment-name] eg: kubectl rollout history deployment my-nginx
```

<h6>Rollback Deployment</h6>

```
kubectl rollout undo deployment [deployment-name] eg: kubectl rollout status deployment my-nginx
```

<h6>Scale the Deployment Pods to 5</h6>
kubectl scale deployment [deployment-name] --replicas=3

## Services

https://kubernetes.io/docs/concepts/services-networking/service/

The Service API, part of Kubernetes, is an abstraction to help you expose groups of Pods over a network. Each Service object defines a logical set of endpoints (usually these endpoints are Pods) along with a policy about how to make those pods accessible.

Since Pods live and die. So we can not rely on a Pod IP address. Services provide a single point of entry for accesing one or more Pods

We have 4 Services type:

- ClusterIP: Exposes the Service on a cluster-internal IP (default).
- NodePort: Exposes the Service on each Node's IP at a static port
- LoadBalancer: Exposes the Service externally using a cloud provider's load balancer
- ExternalName: Maps the Service to the contents of the externalName field (e.g. foo.bar.example.com), by returning a CNAME record with its value. No proxying of any kind is set up

<h6>List Services</h6>

```
kubectl get services
```

<h6>Create Service</h6>

```
kubectl create -f [service-file-name].yml eg: kubectl create -f nginx.deployment.service.yml
```

<h6>Create or modify Service</h6>

```
kubectl apply -f [service-file-name].yml eg: kubectl apply -f nginx.deployment.service.yml
```

<h6>Delete Service</h6>

```
kubectl delete service [name-of-service] eg: kubectl delete -f my-nginx
```

<h6>Get information of Service</h6>

```
kubectl describe service [service-name] eg: kubectl describe service my-nginx
```

<h6>Go to Pod shell, install curl and test a url</h6>

```
kubectl exec [pod-name] –it sh

apk add curl

curl http://podIp
```
