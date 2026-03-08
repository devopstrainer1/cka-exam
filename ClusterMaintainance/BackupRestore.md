# Best practice:  

Create resources declaratively and backup the yaml files in git

## Backup Method 1
Taking immediate backup of all resources:
`kubectl get all -A -o yaml > all-resources.yaml`

restore:
`kubectl apply -f all-resources.yaml`

use Velero (previously ARK) by HeptIO for other resource-components

Method 2:
backup etcd data
In etc service configuration, check the etcd Data Dir. back it up.
![image](https://user-images.githubusercontent.com/17488415/123389271-56631e80-d5b7-11eb-93eb-4a4d48aa1036.png)

Also, edctd Snapshot
`etcdctl snapshot save snapshot.db`

Restore
` service kube-apiserve stop`
```etcctl snapshot restore snapshot.db \
--data-dir /etc/restored-etcd-dir --initial-cluster master=http://masterip:port \
--initial-cluster-token etcd-cluster-new \
--initial-advertise-peer-urls https://${INTERNAL_IP}:2380
```
```
# etcd.service
# add two lines
--initial-cluster-token etcd-cluster-new \
--data-dir /etc/restored-etcd-dir
```
`systemctl daemon-reload`
`service etcd restart`
` service kube-apiserve start`

