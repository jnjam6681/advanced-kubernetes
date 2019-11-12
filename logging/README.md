## Logging
#### Prepare for setting up
Edit volumeClaimTemplates in elasticsearch-statfulset.yaml to your volume.
#### Forward the local
```
kubectl port-forward kibana-pod 5601:5601 --namespace=kube-system
```

## Basic Authentication
#### Creating An htpasswd File
```
htpasswd -c auth foo

New password: <bar>
New password:
Re-type new password:
Adding password for user foo
```
#### Create a Secret
```
kubectl create secret generic basic-auth --namespace=kube-system --from-file=auth
```
```
kubectl get secret basic-auth -o yaml

apiVersion: v1
data:
  auth: Zm9vOiRhcHIxJE9GRzNYeWJwJGNrTDBGSERBa29YWUlsSDkuY3lzVDAK
kind: Secret
metadata:
  name: basic-auth
  namespace: kube-system
type: Opaque
```
#### Modify Ingress
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.class: nginx
    nginx.ingress.kubernetes.io/auth-realm: Authentication Required - monitoring
    nginx.ingress.kubernetes.io/auth-secret: basic-auth
    nginx.ingress.kubernetes.io/auth-type: basic
...
```
#### References
- [`https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/fluentd-elasticsearch`](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/fluentd-elasticsearch)
- [`https://www.digitalocean.com/community/tutorials/how-to-set-up-an-elasticsearch-fluentd-and-kibana-efk-logging-stack-on-kubernetes`](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-elasticsearch-fluentd-and-kibana-efk-logging-stack-on-kubernetes)
- [`https://kubernetes.github.io/ingress-nginx/examples/auth/basic/`](https://kubernetes.github.io/ingress-nginx/examples/auth/basic/)
