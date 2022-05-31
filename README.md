# learn-k8s

Commands

kubeadm token create --print-join-command

kubeadm join 10.182.0.2:6443 --token mg12ua.a6d8f17bppqg2gwf --discovery-token-ca-cert-hash sha256:64c8cbc247e6c4f63b6c4329018ad8ac18f0b7dc4033d4e8080996f0a3e1a148 


list all k8s resources 

    kubectl api-resources 

dry run 

kubectl run nginx-pod  --image nginx --dry-run=client -o yaml

kubectl get pods --all-namespaces

delete all 
 kubectl delete all --all -n <namespace>

inside pod 
 kubectl -n <ps-2> exec -it <set-env> -- bash

Service:
 port: port of pod
 nodePort: cluster level
 targetPort: port of container

edit:
    kubectl edit <deploy> <deployment-name>

################

Rolling update:

kubectl set image deploy <deployment-name> app=<image-name> --record=true

List all revision
kubectl rollout history deploy <deployment-name>

Check status 
kubectl rollout status deploy <deployment-name>

Rollback :

kubectl rollout undo deploy <deployment-name> --to-revision=<revision-number>

################

######################################################################
etcd
######################################################################

--cert-file=            /etc/kubernetes/pki/etcd/server.crt
--trusted-ca-file=      /etc/kubernetes/pki/etcd/ca.crt

--peer-cert-file=       /etc/kubernetes/pki/etcd/peer.crt
--peer-key-file=        /etc/kubernetes/pki/etcd/peer.key
--peer-trusted-ca-file= /etc/kubernetes/pki/etcd/ca.crt

--key-file=/etc/kubernetes/pki/etcd/server.key

mkdir /etcd-backup
ETCDCTL_API=3 etdcl --endpoints=https://10.182.0.2:2379 --cacert /etc/kubernetes/pki/etcd/ca.crt --cert /etc/kubernetes/pki/etcd/server.crt --key /etc/kubernetes/pki/etcd/server.key snapshot save etcd-snapshot-latest.db

############################################
Events:
############################################

kubectl get event --namespace abc-namespace --field-selector involvedObject.name=my-pod-zl6m6



kubectl run rbac-test-pod --image=nginx -n rbac-test-sa:rbac-test --dry-run=client -o yaml 

kubectl config set-context gce --user=cluster-admin --namespace=foo \
  && kubectl config use-context gce


