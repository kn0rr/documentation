# Basics of Kubernetes

## Basic Infrastructure

![Kubernetes Infrastructure](img/Kubernetes.svg)

## Transfer Knowledge

We used for docker-compose and the deployment to AWS a config file to describe what we want to do. The same applies for Kubernetes.

![Config-files](img/Config-Files.svg)


So to transfer the knowledge we have from the docker-compose file take a look at the following:

![Compose-vs-Kubernetes](img/Comparison.svg)

In the picture you see that in case of Kuberentes we are talking about **objects**. 

## Kubernetes Objects and API Versions

![Object-Types](img/Object_Types.svg)

In Kubernetes there exists different kinds of Objects which we want to create through our config-files.

Usage of differenet types:

![Pod_vs_Serivces](img/Pods_vs_Services.svg)

 - **Pod**: A Pod is used for running a container
 - **Services**: Setting up some networking 
 - **Deployment**: Maintains a set of identical pods, ensuring that they have the correct config and that the right number exists

### Pod in Detail:

![POD](img/Pod_Detail.svg)

### Deployment in Detail:

![Deployment](img/Pod_vs_Deployment.svg)
 
### Services in Detail:

![Services](img/Services_Detail.svg)

### API Concept

 In Kubernetes the API version defines a different set of Objects which can be used, so its necessary to know which Object you want to create to specify the API Version:

 ![API-Version](img/K8s-API.svg)

 ## Commands

![apply-config-file](img/K8s_commands.svg)

## Deployment flow

![Deployment_Flow](img/Deployment-Flow.svg)

## Takeaways

![Takeaways](img/K8s_Important_Takeways.svg)

## Imperative vs Declarative

![Imperative_vs_Declarative](img/Imperative_vs_declarative.svg)

## Update an Object Declarative

![Config-Update](img/UpdateConfig.svg)

## How to update an Image Version

![Update_ImageVersion](img/Update_Image_Kubernetes.svg)

We war using the last option with an imperative command.

We need to do the following:

1. Build the new image
2. Push the new image
3. Set new image via imperative command

````docker
docker build -t kn0rr/multi-docker-client:v5 .
docker push kn0rr/multi-docker-client:v5
kubectl set image deployment/client-deployment client=kn0rr/multi-docker-client:v5
````

## Combine two config files into one

````yml
# you can combine confige files and put them together with an ---
apiVersion: apps/v1
kind: Deployment
metadata:
    name: server-deployment
spec:
    replicas: 3
    selector:
        matchLabels:
            component: server
    template:
        metadata:
            labels:
                component: server
        spec:
            containers:
                - name: server
                  image: kn0rr/multi-k8s-server
                  ports:
                    - containerPort: 5000
---
    apiVersion: v1
    kind: Service
    metadata:
        name: server-cluster-ip-Service
    spec:
        type: ClusterIP
        selector: 
            component: server
        ports:
            - port: 5000
              targetPort: 5000

````

# Mulit-Container App with Kubernetes

### Architecture

![Multi-ContainerApp](img/k8s_multiContainerApp.svg)

### Storage Issues

![StorageIssues](img/k8s_StorageIssues.svg)

### K8s Volumes

There exists 3 Types of "Volumes" which Kubernetes is aware of:
1. Volumes: Storage tied to the POD. 

2. Persistent Volumes: Storage outside of the Pod
 
3. Persistent Volume  Claims: It is not a actual instance of Storage instead it is something we attach to a pod config. Kubernetes is trying to find a statical or dynamical provisioned Perstistent volume to meet the requirement of this claim.

![K8sVolumes](img/k8s-volumes.svg)



### Persistent Volume Claims

It is not a actual instance of Storage instead it is something we attach to a pod config. Kubernetes is trying to find a statical or dynamical provisioned Perstistent volume to meet the requirement of this claim.

````yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
    name: database-persistent-volume-claim
spec:
    accessModes:
        - ReadWriteOnce
    resources:
        requests:
            storage: 2Gi
````

#### Access Modes

 1. ReadWriteOnce: Can be used by a **single node**

 2. ReadOnlyMany: **Multiple nodes** can **read** from this

 3. ReadWriteMany: Can be **read and written** to by **many nodes**

