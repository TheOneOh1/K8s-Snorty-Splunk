# K8s-Snorty-Splunk
_________________________________

## PROJECT 

We are going to implement 3 AWS instances imitating as a network. </br>
The instances will be connected by a Kubernetes Cluster as One Master and Two Worker nodes. </br>
We are going to introduce another Instance, a gateway for this AWS Cluster on which IDS will be implemeted, we are using SNORT on it. </br>
This Gateway instance will be an AWS AMI designed specifically for SPLUNK. </br>
We will be protecting the AWS Cluster with SNORT IDS and extracting the IDS logs and with the help of SPLUNK Forwarder, monitor and disply them onto the SPLUNK WebApp. </br>



### TECH USED

- **AWS** &nbsp; <a
href="https://aws.amazon.com/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/93/Amazon_Web_Services_Logo.svg/1280px-Amazon_Web_Services_Logo.svg.png" alt="AWS" width="30" height="20"/> </a></br>
- **KUBERNETES** &nbsp; <a href="https://kubernetes.io/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/kubernetes/kubernetes-icon.svg" alt="kubernetes" width="30" height="30"/> </a> </br>
- **SNORT** &nbsp; <a href="https://www.splunk.com/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/en/3/3a/Snort_ids_logo.png" alt="splunk" width="60" height="40"/> </a> </br>
- **SPLUNK / SPLUNK Forwarder** <a href="https://www.snort.org/" target="_blank" rel="noreferrer"> <img src="https://www.splunk.com/content/dam/splunk2/images/2020-splunk-planet.svg" alt="splunk" width="35" height="35"/> </a></br>

___________________________________________________

**Table of Contents**

<!--ts-->
* [K8s CONFIG](https://github.com/TheOneOh1/K8s-Snorty-Splunk/blob/main/k8s.md#k8s-config)
* [SPLUNK FORWARDER](https://github.com/TheOneOh1/K8s-Snorty-Splunk/blob/main/SplunkForwarder.md#splunk-forwarder)
* [SPLUNK](https://github.com/TheOneOh1/K8s-Snorty-Splunk/blob/main/splunk-snort.md#splunk)
* [SNORT Config](https://github.com/TheOneOh1/K8s-Snorty-Splunk/blob/main/splunk-snort.md#install-snort-on-this-machine)
<!--te-->
