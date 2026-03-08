```
git clone https://github.com/nginxinc/kubernetes-ingress/
cd kubernetes-ingress/deployments/
git checkout v1.11.3
```

```
kubectl apply -f common/ns-and-sa.yaml
kubectl apply -f rbac/rbac.yaml
kubectl apply -f rbac/ap-rbac.yaml
kubectl apply -f common/default-server-secret.yaml
kubectl apply -f common/nginx-config.yaml
kubectl apply -f common/ingress-class.yaml
kubectl apply -f common/crds/k8s.nginx.org_virtualservers.yaml
kubectl apply -f common/crds/k8s.nginx.org_virtualserverroutes.yaml
kubectl apply -f common/crds/k8s.nginx.org_transportservers.yaml
kubectl apply -f common/crds/k8s.nginx.org_policies.yaml
kubectl apply -f common/crds/k8s.nginx.org_globalconfigurations.yaml
kubectl apply -f common/global-configuration.yaml
kubectl apply -f daemon-set/nginx-ingress.yaml
```
```
kubectl get pods --namespace=nginx-ingress --watch
```
```
kubectl create -f service/nodeport.yaml 
kubectl create deployment --image=bitnami/tomcat --port 8080 tomcat
kubectl create deployment --image=httpd --port 80 tomcat
kubectl create deployment --image=httpd --port 80 httpd
kubectl expose deployment tomcat --port 80 --target-port 8080
kubectl expose deployment httpd --port 80 --target-port 80
```
```yaml
# ingress.yaml

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-example
spec:
  rules:
  - http:
      paths:
      - path: /tomcat
        pathType: Exact
        backend:
          service:
            name: tomcat
            port:
              number: 8080
      - path: /httpd
        pathType: Exact
        backend:
          service:
            name: httpd
            port:
              number: 80
```

```yaml
kind: Pod
apiVersion: v1
metadata:
  name: apple-app
  labels:
    app: apple
spec:
  containers:
    - name: apple-app
      image: hashicorp/http-echo
      args:
        - "-text=apple"

---

kind: Service
apiVersion: v1
metadata:
  name: apple-service
spec:
  selector:
    app: apple
  ports:
    - port: 5678 # Default port for image

---

kind: Pod
apiVersion: v1
metadata:
  name: banana-app
  labels:
    app: banana
spec:
  containers:
    - name: banana-app
      image: hashicorp/http-echo
      args:
        - "-text=banana"

---

kind: Service
apiVersion: v1
metadata:
  name: banana-service
spec:
  selector:
    app: banana
  ports:
    - port: 5678 # Default port for image
```
