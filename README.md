# MetalLB

MetalLB used to deploy loadbalancer in local kubernetes cluster


## Installation 

This will create metallb-system namespace and deploy components to your cluster.

The metallb-system/controller deployment. This is the cluster-wide controller that handles IP address assignments.
The metallb-system/speaker daemonset. This is the component that speaks the protocol(s) of your choice to make the services reachable.
Service accounts for the controller and speaker, along with the RBAC permissions that the components need to function.

```
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.5/manifests/namespace.yaml
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.5/manifests/metallb.yaml
# On first install only
kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"
```


## Configuration

To configure MetalLB deploy config map in metallb-system namespace. Before creating config map provide the internal IP addresses range of your kubernetes cluster to allocate the loadbalancer service.

kubectl create -f metallb-cm.yaml
