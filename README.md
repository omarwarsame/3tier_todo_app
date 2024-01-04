### [My GitHub](https://github.com/omarwarsame)
### [My LinkedIn](https://www.linkedin.com/in/owarsame/)
### [Drop me a line](mailto:jubawarsame@gmail.com)
### [My Resume](https://devsom.co.uk/)
# 3 Tier Todo App
***

## PHP To-do application requirements
This app will require database and database management tool

## What this app can do
It can insert data, update data and delete data
***
## Kubernetes

### MYSQL POD
#### Required
1. ConfigMap
2. Secret
3. ClusterIP Service

### PHPMYADMIN POD
#### Required
1. ConfigMap
2. Secret
3. NodePort Service

### PHP Todo App POD
#### Required
1. NodePort Service
***
## DEPLOYMENT PROCESS
### Step 1:
#### MYSQL POD
##### Parameters Required:
1. Database Name
2. Username
3. Password

_Database Name = sqldb_.
_Database User = root_.
_Root Password = rootpassword_.


### STEP 2:
#### PHPMYADMIN POD
##### Parameters Required:
1. Database Name
2. Database Host
3. Database Username
4. Database Password

Link it with MSQL
phpMyAdmin is a Database management tool.


### STEP 3:
#### PHP To-Do App POD
##### Parameters Required:
1. Database Name
2. Database Host
3. Database User
4. User Password.
Link it with MYSQL


***
> "Live as if you were to die tomorrow. Learn as if you were to live forever." – Mahatma Gandhi

## Steps for installation
###Setup for the Master Node
Name your server ‘Master’
Provision t2.medium Ubuntu Linux (Take all the usual steps: keypair, default vpc etc)
Expose all traffic for now (in SG)
Select 30GB for storage

###Setup for the Worker Node
Name your server ‘Node’
Provision t2.medium Ubuntu Linux (Take all the usual steps: keypair, default vpc etc)
Expose all traffic for now (in SG)
Select 30GB for storage

Login to both Master and Worker Node via SSH as a root, put this code in a file called kubeadm.sh and execute with 'sh kubeadm.sh'

```
sudo apt-get update -y
sudo apt-get install \
ca-certificates \
curl \
gnupg -y

sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg -y

echo \
"deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
"$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update -y
echo "To install the latest version, run:"
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

sudo vim /etc/modules-load.d/containerd.conf <<EOF
i
overlay
br_netfilter
Esc
:wq
EOF

modprobe overlay
modprobe br_netfilter

sudo vim /etc/sysctl.d/kubernetes.conf <<EOF
i
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
Esc
:wq
EOF
sudo sysctl --system
sudo sysctl -p

rm -f /etc/containerd/config.toml
systemctl daemon-reload

apt-get update && apt-get install -y apt-transport-https ca-certificates curl -y
curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

swapoff -a

export KUBE_VERSION=1.23.0


apt-get update -y
apt-get install -y kubelet=${KUBE_VERSION}-00 kubeadm=${KUBE_VERSION}-00 kubectl=${KUBE_VERSION}-00 kubernetes-cni=0.8.7-00
apt-mark hold kubelet kubeadm kubectl
systemctl enable kubelet
systemctl start kubelet

```


