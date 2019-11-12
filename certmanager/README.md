## Setting up Cert-Manager
#### Cert-manager helm chart
```
kubectl apply \
    -f https://raw.githubusercontent.com/jetstack/cert-manager/release-0.9/deploy/manifests/00-crds.yaml
```
#### Enable advanced resource validation using a webhook
```
kubectl label namespace kube-system certmanager.k8s.io/disable-validation="true"
```
#### Add the Jetstack helm repository
```
helm repo add jetstack https://charts.jetstack.io
```
#### Install the cert-manager helm chart
```
helm install --name cert-manager --namespace kube-system jetstack/cert-manager
```
#### Get Details
```
kubectl describe certificate
kubectl describe secert
```
#### Reference
[`https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes`](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nginx-ingress-with-cert-manager-on-digitalocean-kubernetes)
