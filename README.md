# How to Install CSF on Ubuntu 20.04
## In this tutorial, you will install CSF on Ubuntu 20.04. CSF is basically ConfigServer Security and Firewall, a popular security tool.

Introduction
Before we begin talking about how to install CSF on Ubuntu 20.04, let’s briefly understand - What is CSF?

CSF is a ConfigServer Security and Firewall. It is a popular security tool for Linux. Further, it provides a simple-interface for the iptables to protect the Linux servers. The CSF has multiple features like stateful packet inspection firewall, intrusion-detection, a login-failure daemon, DDOS-protection, and control-panel integration.

In this tutorial, you will install CSF. We will also answer some FAQs relating to CSF installation.

### Step 1 - Deploying the Ubuntu Server
1) Deploy the new Ubuntu 20.04 instance.

2) Connect to the server through SSH as root.

### Step 2 - Preparing for the CSF Installation
1) Ubuntu 20.04 comes with the UFW firewall by default. You must remove it before installing CSF using the following command:

```
 apt remove ufw
```

2) Next, install the CSF dependencies.

apt install perl zip unzip libwww-perl liblwp-protocol-https-perl
3) The CSF needs Send-mail to send alerts to the administrator.

```
apt install sendmail-bin
```

### Step 3 - Installing the CSF
1) Now, you should navigate to /usr/src.

```
cd /usr/src
```

2) Download the CSF distribution, by using the following command:

```
wget https://download.configserver.com/csf.tgz
```

3) Next extract the CSF.

```
tar -xzf csf.tgz
```

4) Then, navigate to /usr/src/csf.

```
cd csf
```
5) After that, eun the following command:

```
sh install.sh
```
6) Verify necessary iptables modules for the CSF are available.

```
perl /usr/local/csf/bin/csftest.pl
```
7) Now, confirm that all tests report OK. You will notice the below result:

RESULT: csf should function on this server
8) Then, verify CSF status after the installation:

```
csf -v
```

9) You will see the below results:

```
csf: v14.02 (generic)
```

*WARNING* TESTING mode is enabled - do not forget to disable it in the configuration

### Step 4 - Configuring the CSF

1) The CSF runs in the TESTING mode by-default. Next, you need to edit /etc/csf/csf.conf to disable the TESTING mode.

```
nano /etc/csf/csf.conf
```

2) Now, locate the line TESTING = 1. Now, change the value to 0.

```
TESTING = "0"
```

3) You will then locate the line RESTRICT_SYSLOG = 0 and change the value to 3, that means only members of the RESTRICT_SYSLOG_GROUP may access the syslog/rsyslog files. Do it using the following command:

```
RESTRICT_SYSLOG = "3"
```

4) Now, save the configuration file.

5) You will stop and reload the CSF with -ra option:

```
csf -ra
```

Allow all access of all ports

```
vi /etc/csf/csf.allow
```

FAQs to Install CSF on Ubuntu 20.04
1) CSF is not a firewall, but an interface to iptables?
CSF protects the user from the DDOS or jellyfish robots. You can consider security using the iptables.


2) How to check the CSF firewall status?
You will need to have the SSH-login permission to the Server. It will enable to start or stop the CSF. At starting, login to the server via the ssh by a Terminal or Putty. Now, check the status of CSF, by running /etc/init.d/csf status.

