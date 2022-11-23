# K8s-Snorty-Splunk
_________________________________

## PROJECT 

We are going to implement 3 AWS instances imitating as a network. </br>
The instances will be connected by a Kubernetes Cluster as One Master and Two Worker nodes. </br>
We are going to introduce another Instance, a gateway for this AWS Cluster on which IDS will be implemeted, we are using SNORT on it. </br>
This Gateway instance will be an AWS AMI designed specifically for SPLUNK. </br>
We will be protecting the AWS Cluster with SNORT IDS and extracting the IDS logs and with the help of SPLUNK Forwarder, monitor and disply them onto the SPLUNK WebApp. </br>



### TECH USED

- **AWS** </br>
- **Kubernetes** </br>
- **SNORT** </br>
- **SPLUNK / SPLUNK Forwarder** </br>

___________________________________________________

**Table of Contents**

<!--ts-->
* [K8s CONFIG](https://github.com/TheOneOh1/K8s-Snorty-Splunk/blob/main/k8s.md#k8s-config)
* [SPLUNK FORWARDER](https://github.com/TheOneOh1/K8s-Snorty-Splunk/blob/main/SplunkForwarder.md#splunk-forwarder)
* [SPLUNK](https://github.com/TheOneOh1/K8s-Snorty-Splunk/blob/main/splunk-snort.md#splunk)
* [SNORT Config](https://github.com/TheOneOh1/K8s-Snorty-Splunk/blob/main/splunk-snort.md#install-snort-on-this-machine)
<!--te-->
