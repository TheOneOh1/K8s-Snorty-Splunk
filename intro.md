## PROJECT 

We are going to implement 3 AWS instances imitating as a network. The instances will be connected by a Kubernetes Cluster as One Master and Two Worker nodes.
We are going to introduce another Instance as a gateway for this AWS Cluster on which IDS will be implemeted, in this case we are using SNORT.
This Gateway instance will be an AWS AMI designed specifically for SPLUNK.
We will be protecting the AWS Cluster with SNORT IDS and extracting the IDS logs and with the help of SPLUNK Forwarder, monitor and disply them onto the SPLUNK WebApp.



### TECH USED

-**AWS** </br>
-**Kubernetes** </br>
-**SNORT** </br>
-**SPLUNK / SPLUNK Forwarder** </br>

__________________________________________________

## K8s CONFIG

- Installing Docker and Dependancies </br>
``apt-get install ca-certificates curl gnupg lsb-release``

- Add Docker’s official GPG key </br>
``mkdir -p /etc/apt/keyrings`` </br>
``curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg``

- set up the repository: </br>
``echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null``


- Install Docker Engine </br>
``sudo apt-get update`` </br>
``sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin``

- Configure the Docker daemon, in particular to use systemd for the management of
the container's cgroups </br>
``mkdir /etc/docker``  </br>
```
cat <<EOF | sudo tee /etc/docker/daemon.json
{
"exec-opts": ["native.cgroupdriver=systemd"]
}
EOF
``` 
``systemctl enable --now docker`` </br>
``usermod -aG docker ubuntu`` </br>
``systemctl restart docker``  </br>

- Turn off swap space </br>
``swapoff -a``  </br>
``sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab``

- When this is set to 1, bridged packets will traverse iptables rules. This is a requirement for Container Network Interface (CNI) plug-ins to work. </br>
``sysctl net.bridge.bridge-nf-call-iptables=1``

- Install kubectl, kubelet and kubeadm </br>
```
> apt-get update && sudo apt-get install -y apt-transport-https curl

> curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg

> echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

> apt update -y

> apt install -y kubelet kubeadm kubectl

> rm /etc/containerd/config.toml

> systemctl restart containerd

```
