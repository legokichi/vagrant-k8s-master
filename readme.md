

```sh

sudo apt-get install virtualbox
sudo apt-get install vagrant
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://packages.cloud.google.com/apt/ kubernetes-xenial-unstable main" >> ~/kubernetes.list
sudo mv ~/kubernetes.list /etc/apt/sources.list.d
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl kubernetes-cni

```

## reference
### kubernetes
* https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/
* https://github.com/kubernetes/minikube
* https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

### gpu plugin
* https://github.com/Langhalsdino/Kubernetes-GPU-Guide
* https://kubernetes.io/docs/tasks/manage-gpus/scheduling-gpus/
* 
### k8s-device-plugin
* https://blog.sky-net.pw/article/89
* https://deeeet.com/writing/2018/01/15/kubernetes-gpu/
* https://github.com/NVIDIA/k8s-device-plugin

### vagrant
* https://github.com/xbernpa/vagrant-kubernetes-lab
