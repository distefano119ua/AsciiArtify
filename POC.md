Instalatoin ArgoCD on Kubernetes:
preparation:
- wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
- k3d cluster create argo
- **kubectl cluster-info:**
Kubernetes control plane is running at https://0.0.0.0:37555
CoreDNS is running at https://0.0.0.0:37555/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://0.0.0.0:37555/api/v1/namespaces/kube-system/services/https:metrics-server:https/proxy

Install Argo CD:
- kubectl create namespace argocd
- k get ns
NAME              STATUS   AGE
argocd            Active   10s
default           Active   5m52s
kube-node-lease   Active   5m52s
kube-public       Active   5m52s
kube-system       Active   5m52s

- kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
- k get all -n argocd: check cmd
- k get po -n argocd -w: check cmd

Install Argo CD GUI:
- kubectl port-forward svc/argocd-server -n argocd 8080:443&
- change to Port Protovol to HTTPS:
  <img width="783" alt="image" src="https://github.com/user-attachments/assets/f8f7a2c0-a1e7-423d-9021-a382062b2691" />

**Password** to Argo CD GUI:
- kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
