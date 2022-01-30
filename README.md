
# Vagrantfile and Scripts to Automate Kubernetes Setup using Kubeadm [Practice Environemnt for CKA/CKAD and CKS Exams]

## Documentation

Current k8s version for CKA, CKAD and CKS exam: 1.22.

Refer this link for documentation: https://devopscube.com/kubernetes-cluster-vagrant/

## CKA, CKAD, CKS or KCNA Voucher Codes

🚀  If you are preparing for CKA, CKAD, CKS or KCNA exam, save 25% (up to $143) using code **CNYDEVOPS22** at https://kube.promo/cny

## Prerequisites

1. Working Vagrant setup
2. 8 Gig + RAM workstation as the Vms use 3 vCPUS and 4+ GB RAM

## For MAC Users

Latest version of Virtualbox for Mac/Linux can cause issues because you have to create/edit the /etc/vbox/networks.conf file and add:
<pre>* 0.0.0.0/0 ::/0</pre>

So that the host only networks can be in any range, not just 192.168.56.0/21 as described here:
https://discuss.hashicorp.com/t/vagrant-2-2-18-osx-11-6-cannot-create-private-network/30984/23
 
## Usage/Examples

To provision the cluster, execute the following commands.

```shell
git clone https://github.com/scriptcamp/vagrant-kubeadm-kubernetes.git
cd vagrant-kubeadm-kubernetes
vagrant up
vagrant ssh master
vagrant ssh node01
```

## Set Kubeconfig file varaible.

```shell
cd vagrant-kubeadm-kubernetes
export KUBECONFIG=$(pwd)/configs/config
```

or you can copy the config file to .kube directory.

```shell
cp config ~/.kube/
```

## Quick Test
```shell
10.0.0.10 (master)
10.0.0.11 (node01)
10.0.0.11 (node02)

kubectl top nodes
kubectl get po -n kube-system

#Deploy a sample Nginx app and see if you can access it over the nodePort.
kubectl apply -f https://raw.githubusercontent.com/scriptcamp/kubeadm-scripts/main/manifests/sample-app.yaml

http://10.0.0.11:32000
```

## Kubernetes Dashboard URL

```shell
kubectl proxy
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/overview?namespace=kubernetes-dashboard
#use token from configs folder.
```

## Kubernetes login token

Vagrant up will create the admin user token and saves in the configs directory.

```shell
cd vagrant-kubeadm-kubernetes
cd configs
cat token
```

## To shutdown the cluster, 

```shell
vagrant halt
```

## To restart the cluster,

```shell
vagrant up
```

## To destroy the cluster, 

```shell
vagrant destroy -f
```

## Centos & HA based Setup

If you want Centos based setup, please refer https://github.com/marthanda93/VAAS
  
