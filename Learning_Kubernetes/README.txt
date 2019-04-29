::::::::::::::::::
Installation Guide
::::::::::::::::::

Minikube is a method for creating a local, single-node Kubernetes cluster for development and testing. Setup is completely automated and doesn’t require a cloud provider account.

Follow this Link: https://kubernetes.io/docs/setup/minikube/

The Kubernetes command-line tool, kubectl, allows you to run commands against Kubernetes clusters. You can use kubectl to deploy applications, inspect and manage cluster resources, and view logs.

::::::::::::::::::::::::::::::::::
Installing Kubectl on Linux/Ubuntu
::::::::::::::::::::::::::::::::::


Download the latest release with the command:

curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

To download a specific version, replace the $(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt) portion of the command with the specific version.

For example, to download version v1.14.0 on Linux, type:

curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.14.0/bin/linux/


:::::::::::::::::::::
Install Minikube
:::::::::::::::::::::

You can install Minikube on Linux by downloading a static binary:

$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube

Here’s an easy way to add the Minikube executable to your path:

$ sudo cp minikube /usr/local/bin && rm minikube


::::::::::::::::::::::::::::::
Deploying App Using Kubernetes
::::::::::::::::::::::::::::::

$ minikube version

$ minikube start

You now have a running Kubernetes cluster in your terminal. Minikube started a virtual machine for you, and a Kubernetes cluster is now running in that VM.

$ minikube status
minikube: Running
cluster: Running
kubectl: Correctly Configured: pointing to minikube-vm at 192.168.99.100

$ kubectl version

The client version is the kubectl version; the server version is the Kubernetes version installed on the master.

$ kubectl get nodes


$ minikube dashboard

From that, we can create an application using a valid  YAML/JSON content/file, or, manually, from the CREATE AN APP section. Click on the CREATE AN APP tab and provide the following application details:

            The application name is webserver
            The Docker image to use is nginx:alpine, where alpine is the image tag
            The replica count, or the number of Pods, is 3
            No Service, as we will be creating it later.


$ kubectl get deployments

$ kubectl get replicasets

$ kubectl get pods

$ kubectl describe pod  webserver-74d8bd488f-dwbzz

$ kubectl get pods -L k8s-app,label2
$ kubectl get pods -l k8s-app=webserver

$ kubectl get pods -l k8s-app=webserver1

$ kubectl delete deployments webserver

$ kubectl get replicasets
No resources found.

$ kubectl get pods
No resources found.

define webserver.yaml


apiVersion: apps/v1
kind: Deployment
metadata:
  name: webserver
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:alpine
        ports:
        - containerPort: 80


$ kubectl create -f webserver.yaml
deployment "webserver" created

$ kubectl get replicasets

$ kubectl get pods


::::::::::::::::::::::::
Creating Service
::::::::::::::::::::::::

$ kubectl create -f webserver-svc.yaml
service "web-service" created

$ kubectl get service


$ kubectl describe svc web-service

$ minikube ip

$ minikube service web-service
