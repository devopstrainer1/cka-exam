  * Docker Networking - CNM
  * CNI
  * Cluster Networking
![Cluster Networking](https://user-images.githubusercontent.com/17488415/123069727-afed1100-d430-11eb-8c6e-5407b84498e7.png)
* Pod Networking
  *  IP Addesses are uniquely shared among Nodes. 
  *  Each Pod on a Node gets an IP address assigned.
* CNI in kubernetes
* CNI Rules
  * Container Runtime must create network namespace
  * Identify network the container must attach to
  * Container Runtime to invoke Network Plugin (bridge) when container is ADDed.
  * Container Runtime to invoke Network Plugin (bridge) when container is DELeted.
  * JSON format of the Network Configuration
* Get CNIs installed
  * `ls -l /etc/cni/net.d`
  * `ps aux | grep kube-api`
* CNI weave
* IP Address Management - Weave
* Service Networking
* ![Service Networking](https://user-images.githubusercontent.com/17488415/123072311-0e1af380-d433-11eb-8176-15265cf68027.png)
  * uses IP tables in namespaces
  * spread across the host
  * Get Service Ip Address range
  * `ps aux | grep kube-api`
       --service-cluster-ip-range=10.96.0.0/12 
   iptables -L -t nat | grep nginx
* DNS in kubernetes
  * Objectives:
    * Service DNS : nginx-dep.default.svc.cluster.local
    * POD DNS : my-pod.default.pod.cluster.local
* CoreDNS in Kubernetes
* Ingress

* 
