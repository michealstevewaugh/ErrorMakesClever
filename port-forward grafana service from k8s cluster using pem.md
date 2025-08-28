🔹 Step 1: Check Grafana service ports
Run:
```
kubectl get svc grafana -n monitoring -o yaml
```
Look for:
```
ports:
  - port: 80
    targetPort: 3000
```
This means:

Service exposes 80

Container actually runs Grafana on 3000 internally

🔹 Step 2: Port-forward using service port

Since the Service is exposing port 80, forward that one:
```
kubectl port-forward svc/grafana 8080:80 -n monitoring
```

Kubernetes cluster is only accessible from an EC2 server, not directly from your laptop.

That means you need two layers of port-forwarding:

From your laptop → EC2 server (SSH tunnel).

From EC2 server → Kubernetes cluster (kubectl port-forward).

🔹 Option 1: Run port-forward inside EC2 and tunnel to your laptop

SSH into EC2 with port-forward:
```
ssh -i volt_bastion.pem -L 8080:localhost:8080 azureuser@40.120.107.194
```
Inside the EC2 server, run:
```
kubectl port-forward svc/grafana 8080:80 -n monitoring
```
On your laptop, open:
```
http://localhost:8080
````
