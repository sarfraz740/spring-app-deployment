# spring-app-deployment
***********************Spring App Deployment on minikune*************************

detailed steps for creating a Minikube cluster

command to install docker is

sudo apt update && apt -y install docker.io

install Kubectl now with the given link
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x ./kubectl && sudo mv ./kubectl /usr/local/bin/kubectl

install Minikube with the given link

curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/

apt install conntrack
exit
sudo usermod -aG docker $USER && newgrp docker

minikube start --vm-driver=docker

minikube status

kubectl version

kubectl get nodes
*******************************************detail steps of deployment yaml file******************
spring-deployment.yml file:

apiVersion: apps/v1
kind: Deployment
metadata:
  name: spring-deployment
  labels:
    app: spring
spec:
  replicas: 3
  selector:
    matchLabels:
      app: spring-app
  template:
    metadata:
      labels:
        app: spring-app
    spec:
      containers:
        - name: spring-container
          image: adminmindbowser/myinterviewimage:latest
          ports:
            - containerPort: 8080
In this YAML file:

metadata.name :is the name of the deployment.

spec.replicas : is the number of replicas that we want to deploy.

spec.selector.matchLabels.app is the label used to select the pods to manage.

spec.template.metadata.labels.app :is the label used to identify the pods in the deployment.

spec.template.spec.containers.name :is the name of the container.

spec.template.spec.containers.image :is the Docker image that we want to use.

spec.template.spec.containers.ports.containerPort :is the port that our application will be running on

******************************************detail steps of service yaml file*************************************
apiVersion: v1

kind: Service

metadata:
  name: my-app-service

spec:
  type: NodePort
  
  selector:
    app: spring-app
  ports:
    - name: http
      port: 8080
      targetPort: 8080
      nodePort: 30000 # you can choose any port in the range 30000-32767




