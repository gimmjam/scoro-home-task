# scoro-home-task

# Task1:
Details are given inside /cluster/cluster-creation.txt

# Task2:
yaml files are located inside /templates/..
First setup Helm and Kubernetes 

Download Helm:
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

Make the script executable:  
$ chmod 700 get_helm.sh

Run following script to ensure Helm is installed correctly:  
$ ./get_helm.sh  
$ helm version  

Output will look like this  
version.BuildInfo{Version:"v3.14.2", GitCommit:"c309b6f0ff63856811846ce18f3bdc93d2b4d54b", GitTreeState:"clean", GoVersion:"go1.21.7"}

#Add the official Helm stable charts repository:  
$ helm repo add stable https://charts.helm.sh/stable  
$ helm repo update  

To Deploy OWASP Juice Shop  
The yaml files uses the Helm chart templating syntax ({{ .Values.variableName }}) for variables.
1. Package helm chart and get juice-shop-chart.tgz file: $ helm package .
2. Deploy OWASP Juice shop: $ helm install juice-shop-release juice-shop-chart.tgz

Alternatively following commands can be used if Helm is not used
1. Ensure cluster is ready : $ kubectl get  nodes
2. Launch deployment yaml: $ kubectl create -f juice-shop-deployment.yaml 
3. Ensure pod is running: $ kubectl get deployment
4. Launch service: $ kubectl create -f juice-shop-service.yaml 
5. Check service and get value of node port: $ kubectl get svc juice-shop
6. Check endpoints: $ kubectl get ep juice-shop
7. Get node IP: $  kubectl get no -o wide
8. curl node IP and node port from steps #5 and #7: $ curl IP:Node
9. Open browser and launch IP:Node to see the owasp juice shop web application