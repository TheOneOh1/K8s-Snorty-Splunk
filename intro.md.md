## PROJECT 

We are going to implement 3 AWS instances imitating as a network. The instances will be connected by a Kubernetes Cluster as One Master and Two Worker nodes.
We are going to introduce another Instance as a gateway for this AWS Cluster on which IDS will be implemeted, in this case we are using SNORT.
This Gateway instance will be an AWS AMI designed specifically for SPLUNK.
We will be protecting the AWS Cluster with SNORT IDS and extracting the IDS logs and with the help of SPLUNK Forwarder, monitor and disply them onto the SPLUNK WebApp.



### TECH USED

**- AWS**
**- Kubernetes**
**- SNORT**
**- SPLUNK / SPLUNK Forwarder**

__________________________________________________

## K8s CONFIG

- Installing Docker and Dependancies
``apt-get install ca-certificates curl gnupg lsb-release``

- Add Docker’s official GPG key
``mkdir -p /etc/apt/keyrings``

``curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg``

- set up the repository:
``echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null``


- Install Docker Engine
	``sudo apt-get update``

	``sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin``


- Configure the Docker daemon, in particular to use systemd for the management of
the container's cgroups
``mkdir /etc/docker``

``cat <<EOF | sudo tee /etc/docker/daemon.json
``{``
``"exec-opts": ["native.cgroupdriver=systemd"]``
``}``
``EOF``

``systemctl enable --now docker``

``usermod -aG docker ubuntu``

``systemctl restart docker``

- Turn off swap space
``swapoff -a``

``sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab``

- When this is set to 1, bridged packets will traverse iptables rules. This is a requirement for Container Network Interface (CNI) plug-ins to work.
``sysctl net.bridge.bridge-nf-call-iptables=1``

- Install kubectl, kubelet and kubeadm
``apt-get update && sudo apt-get install -y apt-transport-https curl``

``curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg``

``echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list``

``apt update -y``

``apt install -y kubelet kubeadm kubectl``

``rm /etc/containerd/config.toml``

``systemctl restart containerd``