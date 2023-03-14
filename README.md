# GitOps

**Brugt guide:** https://www.arthurkoziel.com/setting-up-argocd-with-helm/  
namespace sat til "argocd"


## For at køre projektet på kubernetes-cluster:  
**Hent projekt ned og cd ind i mappen...**   

**Opret charts og hent dependencies**  
`helm repo add argo-cd https://argoproj.github.io/argo-helm`  
`helm dep update charts/argo-cd/`  

**installer Argo**  
`helm install argo-cd charts/argo-cd/ --create-namespace --namespace argocd`  

**Port forward** (kun hvis ingress ikke er sat op)  
`kubectl port-forward svc/argo-cd-argocd-server -n argocd 8080:443`  
`kubectl port-forward svc/argo-cd-argocd-server --address 0.0.0.0 -n argocd 8080:443`  

**Få adgangskode**  
`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`  

**Kør GitOps-setup i Argo**  
`helm template apps/ | kubectl apply -n argocd -f -`  
