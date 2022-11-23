# SPLUNK FORWARDER

- Now we want to forward these Logs to the SPLUNK dashboard for that we will need the Splunk Universal Forwarder

- Create an account on https://www.splunk.com/
- Download the Splunk Universal Forwarder from https://www.splunk.com/en_us/download/universal-forwarder.html


### On TERMINAL

``wget <link-universal-forwarder.rpm>``

**[Install Splunk Forwarder with rpm]**

``cd /opt/``

``rpm -i splunkforwarder-9.0.1-82c987350fde-linux-2.6-x86_64.rpm``

``cd splunkforwarder/bin/``

``sudo ./splunk start --accept-license``

**NOTE :** This will ask you for credentials, provide the SPLUNK credentials you got with SPLUNK AMI

``sudo ./splunk add forward-server <public-IP>:9997``


``sudo nano /opt/splunkforwarder/etc/system/local/outputs.conf``

	[tcpout]
	defaultGroup = default-autolb-group
	[tcpout:default-autolb-group]
	server = <public-IP>:9997
	[tcpout-server://<public-IP>:9997]

Save and exit the Nano

``cd /opt/splunkforwarder/bin/``

``sudo ./splunk add monitor /var/log/snort/alert``

**[Will ask for SPLUNK username and pass provide the same]**

``sudo nano /opt/splunkforwarder/etc/apps/search/local/inputs.conf``

	[splunktcp://9997]
	connection_host = <public-IP>
	[monitor:///var/log/snort/alert]
	disabled = false
	index = main
	sourcetype = snort_alert_full
	source = snort

Save and exit nano

``cd /opt/splunkforwarder/bin/``

``sudo ./splunk restart``

**NOW go to SPLUNK web portal** *http://public-IP:8000*

1. Click on Search and Reporting.

2. Click on Data Summary, under that you will the HOST that we added.

3. Click on the Host you will see the logs.

![](https://github.com/TheOneOh1/K8s-Snorty-Splunk/blob/main/splunk_dashboard.PNG)

- We also used the **Snort Alert for Splunk** which shows the logs in formatted way

![](https://github.com/TheOneOh1/K8s-Snorty-Splunk/blob/main/snort_dashboard.PNG)
