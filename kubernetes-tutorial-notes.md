# Nana Youtube Video Github repository link for kubernetes tutorial

`https://gitlab.com/nanuchi/youtube-tutorial-series/-/tree/master/demo-kubernetes-components`

# Need for container orchestration tool
----------------------------------------------------------------

 -> Trend from Monolith to Microservices
 -> Increased usage of containers
 -> Deman for a proper way of managing those hundreds of containers


# What features do orchestration tools offer?
----------------------------------------------------------------

-> High availability or no downtime
-> Scalability or high prformance
-> Disaster Recovery 

# We must have more than one replica of master nodes should be available, because master nodes are very important
to track the worker nodes, once if we loose the track of master nodes then we won't be able to talk
to worker  nodes


# what is POD
pod is small deployment unit which runs in kubenetes like a database is one pod, nodejs is another pod, etc.. so each application can have it's own pod and run independently.

Each pod has it's own IP address and port number, they communicate each other using internal IP address and port number.

POD is compoennt of kubernetes, 

https://www.youtube.com/watch?v=Krpb44XR0bk&list=PLy7NrYWoggjziYQIDorlXjTvvwweTYoNC&index=2&ab_channel=TechWorldwithNana



# Main components of Kubernetes:

1. Pods
2. Service
3. Ingress
4. ConfigMap
5. Secrets
6. Volumes
7. Statefulset


# What is Minikube and Kubectl

# Minikube
Minikube is a tool that enables users to run Kubernetes clusters locally on their development machines. It creates a single-node Kubernetes cluster within a virtual machine (using a hypervisor like VirtualBox, HyperKit, or KVM) on the local system. Minikube is primarily used for local development, testing, and learning purposes. It allows developers to experiment with Kubernetes features and deploy applications locally before deploying them to production clusters. Minikube provides an easy way to set up and manage a Kubernetes environment without the need for a full-fledged cluster setup.


# Kubectl

This is the command-line interface (CLI) tool for Kubernetes. It allows users to execute commands against Kubernetes clusters. With kubectl, you can create, inspect, update, and delete Kubernetes resources such as pods, deployments, services, and more. It serves as the primary means for developers and administrators to interact with Kubernetes clusters. Users can manage multiple clusters using kubectl by configuring it to connect to different clusters.

# How to start the minikube cluster

`minikube start --driver=docker`

# Get nodes
`kubectl get nodes`

# Get pods
`kubectl get pods`
`kubectl get pod`

# Get services
`kubectl get services`

# Minikube status

`minikube status`

`kubectl version`

# Creae a deployment with ngnix docker image
`kubectl create deployment nginx-depl --image=nginx`
`kubectl create deployment mongo-depl --image=mongo`

# get the deployment 
`kubectl get deployment`

# get replicat set the deployment
`kubectl get replicaset`

# How to edit the deployment file through kubectl

`kubectl edit deployment nginx-depl`

# How to debug the pod if something is not working

# How to connect to container and run the commands against the application running environment
The below comand lets you connect to the application running terminal and you can do different things
`kubectl exec -it mongo-depl-79585f75cf-bcxnz -- bin/bash `

# How to delete the deployment 
`kubectl delete deployment mongo-depl`

Note: Passing all the configuration details through command prompt while creating a deployment is impossible, to avoid that, Kubctl takes input as yaml file which is configuration-detais.yaml file where environment related configuration are intrustrcuted and kubectl just takes it and executes against the environment and do the set-up for us.

Command to execute it is:

`kubectl apply -f config-file.yaml`

# To open the nginx server from the browser, if we have kubectl installed then we can run the following command to open automatically in the browser

`minikube service nginx-service`

# Get the list of services running by running the following command

`kubectl get services`

# Describing aobut the services

`kubectl describe service nginx-service`

# Get more informatiion about the pods such as Ip address of each pod etc..

`kubectl get pod -o wide`



# Complete application set-up in kubernetes

How to store the secrets in Kubernetes : we can have a dedicated secret file in the kubernetes and read the secrets from it, 
Ex: 
`apiVersion: v1
kind: Secret
metadata:
    name: mongodb-secret
type: Opaque
data:
    mongo-root-username: dXNlcm5hbWU=
    mongo-root-password: cGFzc3dvcmQ=`

All the secrets must be stored  in base64 format only, and below is the command to get the base64 string from the plain text..


`echo -n 'username' | base64`

# Command to apply the secrets into kubernetes using kubectl

`kubectl apply -f mongo-secrets.yaml`


# command to get the secrets list but not shown in termainl is

`kubectl get secrets`

# Command to get all the things in kubernetes 
`kubectl  get all`
ß
# What is the namespace in kubernetes and why is it used for?

`Namespace is used for resource grouping pods individually and easy to understand their serving purpose, let's say, we can have namespace like 'database namespace' where all database related pods are installed similary for log monitoring tools etc.. and ngnix etc.`

# How to create a namespace in kubernets cluster

`kubectl create namespace my-namespace`

`kubectl get namespaces`

`kubectl apply -f my-resource.yaml -n my-namespace`

`kubectl config set-context --current --namespace=my-namespace`

`kubectl delete namespace my-namespace`



# HELM Explained

