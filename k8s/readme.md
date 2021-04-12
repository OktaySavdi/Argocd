**#Install Argocd on Kubernetes**
```
kubectl create namespace argocd
```
```
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
**#set nodeport**
```
kubectl edit svc argocd-server (NodePort)
```
**#get secret for console**
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
**#example1**
```
Repository : https://github.com/argoproj/argocd-example-apps.git
Path       : guestbook
Namespace  : default
```
**#example2**
```
Repository : https://github.com/OktaySavdi/gitops-example.git
Path       : k8s
Namespace  : gitops-dev
```
