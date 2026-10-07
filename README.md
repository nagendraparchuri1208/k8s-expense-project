Your first Kubernetes resource for the Expense project is created successfully:
namespace/expense created

So now your project has:
EKS Cluster
    |
    └── expense namespace

Verify it:
kubectl get namespace expense

[ec2-user@ip-172-31-45-125 k8s-expense-project]$ kubectl get namespace expense
NAME      STATUS   AGE
expense   Active   3m53s

for Mysql:
pod to pod communication 
we need use Service resource.
its purely internal communication for thats why i am using Cluster IP.

for backend we need backend configuration
so, here we need use ConfigMap

frontend---> loadbalancer service
