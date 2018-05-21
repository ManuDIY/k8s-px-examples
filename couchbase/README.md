# Couchbase Cluster on Kubernetes
The files in this directory can serve as an example of how to deploy a Couchbase Server cluster on Kubernetes. Tested on GKE, Amazon as well as a self-deployed Kubernetes cluster.
== Usage
It should be noted at the beginning that this setup depends on KubeDNS to be enabled and functional to successfully deploy.
# Create the Service
+
```
kubectl apply -f couchbase-service.yml
```
+
This file will provision a LoadBalancer for the Web Console of the master node as well.
+
# Create the StorageClass
+
```
kubectl apply -f create -f couchbase-sc.yaml
```

#Create the StatefulSet
+
```
kubectl apply -f couchbase-statefulset-with-stork.yml
```
+
+
. Once the master is up and LB has been provisioned, connect to the WebUI by going to `$LOADBALANCER_IP:8091` in your browser
. Create either auto-rebalancing nodes or just attach the nodes to the cluster with one of the two worker files:
. Scale workers with the normal scaling commands for the StatefulSet
+
```
kubectl scale statefulset couchbase --replicas=3
```
#Build your own image
. Create the image with `docker build -t $DESIRED_IMG_NAME .`
. Update all `.yml` files with your new image name if necessary.