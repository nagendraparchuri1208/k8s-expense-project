The project flow:
----------------
                    Internet
                       |
                       v
              AWS LoadBalancer :80
                       |
                       v
             Frontend Service :80
                       |
                       v
             Frontend Pods :8080
                       |
                 /api/ request
                       |
                       v
             Backend Service :8080
                       |
                       v
             Backend Pods :8080
                       |
                       v
               MySQL Service :3306
                       |
                       v
                MySQL Pods

What your README should make clear
1. Namespace
expense

All project resources are deployed inside this namespace.
2. MySQL
Deployment: mysql
Replicas: 3
Service: mysql
Service Type: ClusterIP
Port: 3306
TargetPort: 3306

Backend connects to MySQL using:
DB_HOST=mysql

because mysql is the Kubernetes Service name.
3. Backend
Deployment: backend
Replicas: 3
Image: joindevops/backend:v1

Service: backend
Type: ClusterIP
Port: 8080
TargetPort: 8080

4. Frontend
Deployment: frontend
Replicas: 2
Image: joindevops/frontend:v1.0

Service: frontend
Type: LoadBalancer
Port: 80
TargetPort: 8080

So:
AWS LoadBalancer :80
        ↓
Frontend Service :80
        ↓
Frontend Pod :8080

5. Frontend → Backend
Your Nginx configuration explicitly has:
location /api/ {
    proxy_pass http://backend:8080/;
}

So:
Browser
   ↓
Frontend :80
   ↓
Nginx :8080
   ↓
backend:8080
   ↓
Backend Pods

Project structure
k8s-expense-project/
│
├── namespace.yaml
│
├── mysql/
│   └── manifest.yaml
│
├── backend/
│   └── manifest.yaml
│
└── frontend/
    └── manifest.yaml

                
