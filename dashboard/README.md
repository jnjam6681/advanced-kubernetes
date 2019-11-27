## Setting up the dashboard
#### Install Metrics Server
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install --name metrics-server bitnami/metrics-server
```
#### Create Dashboard
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml
```
#### Create ServiceAccount
```
kubectl apply -f ./create-user/dashboard-service-account-user.yaml
```
#### Create ClusterRoleBinding
```
kubectl apply -f ./create-user/dashboard-cluster-role-binding-user.yaml
```
#### Get Bearer Token
```
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')
```
#### To Access Dashboard
```
kubectl proxy
```
#### Connect To Dashboard
[`http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/`](
http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/)
#### References
- [`https://github.com/helm/charts/tree/master/stable/kubernetes-dashboard`](https://github.com/helm/charts/tree/master/stable/kubernetes-dashboard)
- [`https://github.com/kubernetes/dashboard/tree/v2.0.0-beta5/aio/deploy/recommended`](https://github.com/kubernetes/dashboard/tree/v2.0.0-beta5/aio/deploy/recommended)
- [`https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md`](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md)
