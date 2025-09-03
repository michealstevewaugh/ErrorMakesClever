🔹 Step 1: Check prometheus-server service ports
Run:
```
kubectl get svc prometheus-server -n monitoring -o yaml
```
Look for:
```
ports:
  - port: 9090
```
This means:

Service exposes 9090

🔹 Step 2: Port-forward using service port

Since the Service is exposing port 9090, forward that one:
```
kubectl port-forward svc/prometheus-server 8082:9090 -n monitoring
```
If you don’t want to keep a terminal open(running back ground):
```
nohup kubectl port-forward svc/prometheus-server 8082:9090 -n monitoring >/dev/null 2>&1 &
```
Kubernetes cluster is only accessible from an EC2 server, not directly from your laptop.

That means you need two layers of port-forwarding:

From your laptop → EC2 server (SSH tunnel).

From EC2 server → Kubernetes cluster (kubectl port-forward).

🔹 Option 1: Run port-forward inside EC2 and tunnel to your laptop

SSH into EC2 with port-forward:
```
ssh -i volt_bastion.pem -L 8082:localhost:8082 azureuser@40.120.107.194
```
If you don’t want to keep a terminal open, run it with -N -f:
```
ssh -i volt_bastion.pem -L 8082:localhost:8082 azureuser@40.120.107.194 -N -f
```
Inside the EC2 server, run:
```
kubectl port-forward svc/prometheus-server 8082:9090 -n monitoring
```
On your laptop, open:
```
http://localhost:8081
````
