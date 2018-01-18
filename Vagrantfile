# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 1.6.0"

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.define "k8smaster" do |config|
    config.vm.hostname = "k8smaster"
    config.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", "1024"]
      v.customize ["modifyvm", :id, "--cpus", "1"]
    end
    config.vm.network :private_network, ip: "192.168.8.10"
    config.ssh.forward_agent = true
    config.vm.provision "shell", inline: <<-SHELL
      set -e
      set -x
      sed 's/127\.0\.0\.1.*k8s.*/192\.168\.8\.10 k8smaster/' -i /etc/hosts
      #echo "192.168.8.11	k8sworker" >> /etc/hosts
      curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
      #echo "deb http://apt.kubernetes.io/ kubernetes-xenial unstable" >> ~/kubernetes.list
      echo "deb https://packages.cloud.google.com/apt/ kubernetes-xenial-unstable main" >> ~/kubernetes.list
      mv ~/kubernetes.list /etc/apt/sources.list.d
      apt-get update
      apt-get upgrade -y
      apt-get install -y docker.io
      apt-get install -y kubelet kubeadm kubectl kubernetes-cni
      echo "export KUBERNETES_SERVICE_HOST=192.168.8.10" > /etc/profile.d/kubernetes.sh
      echo "export KUBERNETES_SERVICE_PORT=6443" >> /etc/profile.d/kubernetes.sh
      echo "export KUBECONFIG=/vagrant/kubeconfig/admin.conf" >> /etc/profile.d/kubernetes.sh
      ###kubeadm init --apiserver-advertise-address 192.168.8.10 --pod-network-cidr 10.244.0.0/16 --kubernetes-version v1.7.1 --token 54c315.78a320e33baaf27d 
      # Rename the cluster to something simpler
      sed -i s,kubernetes-admin@kubernetes,local, /etc/kubernetes/admin.conf
      cp -rf  /etc/kubernetes/admin.conf /vagrant/kubeconfig/      
      export KUBECONFIG=/etc/kubernetes/admin.conf
      ###kubectl patch daemonset kube-proxy -n kube-system --type='json' -p='[{"op": "add", "path": "/spec/template/spec/containers/0/command/2", "value":"--proxy-mode=userspace"}]'
      sleep 60
      # Flannel 
      ###kubectl create -f /vagrant/networking/kube-flannel.yml
    SHELL
  end
end
