\# XOPS Kubernetes App – Custom NGINX Deployment using kind



This Micro challenge sets up a local Kubernetes cluster using \[kind (Kubernetes-in-Docker)](https://kind.sigs.k8s.io/) and deploys a custom NGINX web app using YAML manifests.  

Ideal for learning Kubernetes concepts and exploring core control plane components.



Project Structure.......



&nbsp;   \* File                - Purpose



'README.md'  - Full project guide with K8s concept summary  

'Screenshots' - App running, svc output, etc.                

'app.yaml' - Kubernetes Deployment + Service manifest     

'Docker file' -Builds a custom NGINX image with a new HTML page

'index.html' - Custom NGINX welcome page



\# Step-by-Step Setup



1. Prerequisites



Install the following:



\- \[Docker](https://docs.docker.com/get-docker/)

\- \[kind](https://kind.sigs.k8s.io/)

\- \[kubectl](https://kubernetes.io/docs/tasks/tools/)



&nbsp;2. Build Docker Image



Build your custom NGINX image using - 'docker build -t xops-web:custom .'





&nbsp;3.Create a Local Cluster using - 'kind create cluster --name xops-cluster'



4. Load Image into kind using - 'kind load docker-image xops-web:custom --name xops-cluster'



5. Apply the Kubernetes YAML using - 'kubectl apply -f app.yaml'



6. Verify Deployment using - 'kubectl get pods' \& 'kubectl get svc'



expected output should be :

NAME        TYPE       CLUSTER-IP     PORT(S)        AGE

xops-web     NodePort    10.96.46.213   <none>        80:30007/TCP   28s


7. To access the app

Forward service port (optional for local test) using - 'kubectl port-forward svc/xops-web 8080:80'


Now visit:

&nbsp;http://localhost:8080



.......You should see your custom NGINX welcome page........




To Explore the Kubernetes Components

Run the following commands to inspect the cluster:  



kubectl get pods -A

kubectl get nodes

kubectl get componentstatuses

kubectl describe node
---



*Explained Kubernetes Components:

(a) Master components:

 =>etcd                                          

 =>API server                                      

 =>Scheduler                                

 =>Controller Manager

 (b) Slave Components:

 =>Kubelet
 
 =>Kube-Proxy

Explaination:

=>etcd: It is a highly available distributed key value store, which is used to store cluster wide secrets.

It is only accessible by Kubernetes API server, as it has sensitive information.

=>API Server: API Server exposes the Kubernetes API. The Kubernetes API is the front-end for

Kubernetes Control Plane, and is used to deploy and execute all operations in Kubernetes



=> Scheduler: The scheduler takes care of scheduling of all the processes, Dynamic Resource

Management and manages present and future events on the cluster .



=> Controller Manager: The controller manager, runs all the controllers on the Kubernetes Cluster.
Although each controller, is a separate process, but to reduce complexity,all the controllers are compiled into a single process.
They are as follows:
Node Controller, Replication Controller, Endpoints Controller, Service Accounts and Token Controllers.


=>Kubelet: Kubelet takes the specification from the API server, and ensures the application is running according to the
specifications which were mentioned. Each node has it’s kubelet service.



=> Kube-Proxy: This proxy service runs on each node and helps in making services available to the external host.
It helps in connection forwarding to the correct resources, it is also capable of doing primitive load balancing.



---

#Clean Up using:

'kind delete cluster --name xops-cluster'


Author:

||Ajith Kumar||









