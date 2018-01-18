

```sh

sudo apt-get install virtualbox
sudo apt-get install vagrant
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://packages.cloud.google.com/apt/ kubernetes-xenial-unstable main" >> ~/kubernetes.list
sudo mv ~/kubernetes.list /etc/apt/sources.list.d
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl kubernetes-cni

```

