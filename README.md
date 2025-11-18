# Apache-and-k3s-
## step for installing k3s 
 ### Install K3s
    curl -sfL https://get.k3s.io | sudo sh -
### Create a deployment file for Apache
   #### Create a file:
         nano apache.yaml
   #### Paste the YAML below:
   
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: apache-deployment
    spec:
      replicas: 1
     selector:
        matchLabels:
          app: apache
     template:
        metadata:
      labels:
        app: apache
    spec:
      containers:
      - name: apache
        image: httpd:latest
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: apache-service
spec:
  type: LoadBalancer
  selector:
    app: apache
  ports:
  - port: 80
    targetPort: 80
#### Deploy Apache to K3s
sudo kubectl apply -f apache.yaml
#### Access Apache
sudo kubectl get svc apache-service
<img width="958" height="506" alt="apache and k3s" src="https://github.com/user-attachments/assets/deccb370-de50-4767-9c27-9074e0d92fa6" />


