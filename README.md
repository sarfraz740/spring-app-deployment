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
   In this YAML file:
   
   The kind field indicates that this is a Service object. The metadata section contains information about the Service such as its name, which in this 
   
   case is "my-app-service".

The spec section specifies the Service's specifications, including its type which is set to NodePort. NodePort is a type of Service that exposes the 

Service on a port on each node in the cluster. This allows external traffic to reach the Service by hitting the nodes' IP addresses and the specified 

nodePort value.

The selector field is used to identify the pods that this Service will target. In this case, the Service is targeted at pods with the label app: spring-

app.

The ports section lists the ports that the Service will use. In this case, there is only one port named http with a port value of 8080, a targetPort 

value of 8080 and a nodePort value of 30000. This means that the Service will be accessible on port 30000 of the nodes in the cluster and will forward 

traffic to port 8080 on the pods targeted by the selector field.
   
   
      
      
      
      
      
      
      
      
      
      
      
      
  ***************************pod log details**********************    
        .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v2.4.4)

2023-02-16 17:12:14.055  INFO 1 --- [           main] com.springbootwebdemo.App                : Starting App v0.0.1-SNAPSHOT using Java 1.8.0_212 on spring-deployment-886f4c88c-7mvrs with PID 1 (/springbootwebdemo.war started by root in /)
2023-02-16 17:12:14.060  INFO 1 --- [           main] com.springbootwebdemo.App                : No active profile set, falling back to default profiles: default
2023-02-16 17:12:18.953  INFO 1 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2023-02-16 17:12:18.981  INFO 1 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2023-02-16 17:12:18.981  INFO 1 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.44]
2023-02-16 17:12:21.151  INFO 1 --- [           main] org.apache.jasper.servlet.TldScanner     : At least one JAR was scanned for TLDs yet contained no TLDs. Enable debug logging for this logger for a complete list of JARs that were scanned but no TLDs were found in them. Skipping unneeded JARs during scanning can improve startup time and JSP compilation time.
2023-02-16 17:12:21.350  INFO 1 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2023-02-16 17:12:21.350  INFO 1 --- [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 7070 ms
2023-02-16 17:12:22.261  INFO 1 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2023-02-16 17:12:22.897  INFO 1 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2023-02-16 17:12:22.935  INFO 1 --- [           main] com.springbootwebdemo.App                : Started App in 9.923 seconds (JVM running for 11.629)

      
      
      
      
      
      
      




