Create sock-shop namespace and deploy microservices-demo
```
kubectl create ns sock-shop
kubectl apply -f https://raw.githubusercontent.com/microservices-demo/microservices-demo/master/deploy/kubernetes/complete-demo.yaml
```

create monitoring namespace and deploy prometheus operator using helm
```
kubectl create ns monitoring
helm install stable/prometheus-operator --name=prom --namespace=monitoring
```

add the additional service monitors
```
helm upgrade prom stable/prometheus-operator --values=additionalServiceMonitors.yaml
```

Check if prometheus is scraping logs
```
kubectl port-forward -n monitoring prometheus-prom-prometheus-operator-prometheus-0 9090:9090
```
```
http://localhost:9090
```