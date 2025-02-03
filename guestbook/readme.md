kubectl create namespace argocd

# Install ArgoCD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
#Wait for all pods to be ready:

kubectl wait --for=condition=Ready pod -l app.kubernetes.io/name=argocd-server -n argocd
#Get the initial admin password:

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
#Port forward the service:

kubectl port-forward svc/argocd-server -n argocd 8080:443
#Now try accessing ArgoCD at 

https://localhost:8080


![image](https://github.com/user-attachments/assets/e33e3f94-9d9b-43fb-ab54-026667ff7f07)

My first ArgoCD Deployment
