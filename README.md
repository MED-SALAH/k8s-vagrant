vagrant init
vagrant status
vagrant up -- to start the install of machines

To access to machine : vagrant ssh "nameofmachine"
example:
vagrant ssh kubmaster 

Or you can use vagrant private key for eache machine:
vagrant ssh-config

After preaparing machines :

desactivate Swap:
swapof -a
vim /etc/fstab 
comment ligne of swap with #/dev/mapper/.....swap
mount -a

to check : df -hv 

Nos machines have alerady docker installed in Vagrantfile
add docker user to group sudo :
sudo usermod -aG docker SUSER
* prérequis : installation de docker

systemctl daemon-reload && systemctl restart docker

-> Kubernetes : installation  <-

Installation de kubeadm, des kubelets et de kubectl

cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kube*
EOF

# Mettre SELinux en mode permissif (le désactiver efficacement)
setenforce 0
sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config

yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
-------> yum install -y kubelet kubeadm kubectl kubernetes-cni
systemctl enable --now kubelet 

* initilisation sur le master

# Setup required sysctl params, these persist across reboots.
cat > /etc/sysctl.d/99-kubernetes-cri.conf <<EOF
net.bridge.bridge-nf-call-iptables  = 1
net.ipv4.ip_forward                 = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF

sysctl --system

```
kubeadm init --apiserver-advertise-address=192.168.1.30 --node-name $HOSTNAME --pod-network-cidr=10.244.0.0/16
```
To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
