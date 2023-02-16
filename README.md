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
*******************************************detailed steps of deployment and service yaml file******************

