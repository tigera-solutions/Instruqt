---
slug: container-threat-detection
id: awnosylrjnfj
type: challenge
title: Checking for suspicious process names and args
teaser: Leverage eBPF to monitor syscalls occurring in the cluster.
notes:
- type: image
  url: ../assets/module05.png
tabs:
- title: Shell
  type: terminal
  hostname: controlplane
- title: Calico Cloud
  type: website
  hostname: controlplane
  url: https://www.calicocloud.io/home
  new_window: true
difficulty: basic
timelimit: 900
---
Calico Cloud provides a threat detection engine that analyzes observed files and process activities to detect known malicious threats and suspicious activities.

Enable container threat detection
================

Container threat detection is disabled by default. Let's enable it.

- To enable Container threat detection on your managed cluster, go to the **Threat Defence section** in the Calico Cloud UI, and select **Enable Container Threat Detection**.

![Image Description](../assets/enable-container-threat-detection.png)

- Change the default aggregation period

The default configuration of the runtime-reporter has an aggregation period of 15 minutes [period: 15m]. In order to expedite testing, we will reduce this to 15 seconds.

**NOTE: These changes are for demonstration purposes only and should not be used in a production environment without consulting the support team.**

```bash
kubectl -n tigera-runtime-security annotate daemonset runtime-reporter unsupported.operator.tigera.io/ignore="true"
kubectl -n tigera-runtime-security get daemonset.apps/runtime-reporter -o yaml | sed 's/15m/1m/g' | kubectl apply -f -
```


Triggering malicious activity
================

Calico Cloud detects threats across the entire killchain. This example will focus on privilege escalation tactics like Linux-Administrative-Command and Set-Linux-Capabilities, in addition to executing some attack tools as part of the execution stage.

Linux-Administrative-Command: A pod was detected executing Linux administrative commands using superuser privileges.
Set-Linux-Capabilities: A pod was detected executing commands on the system to modify a file, user, or group capabilities.

- Let's start by deploying a test pod.

```bash
kubectl run multitool --image=wbitt/network-multitool
```

- Now, it's time to execute suspicious processes and activities inside the container.

```bash
kubectl exec -it multitool -- bash
```

- Linux-Administrative-Command example

```bash
adduser joseph
su -
add user joseph
chown joseph file.txt
```

- Set-Linux-Capabilities example

```bash
touch file.txt
setcap cap_net_raw+ep file.txt
```

- Attack tools example

```bash
nmap -Pn -r -p 1-900 $POD_IP
```

- View the alerts in Calico Cloud UI. From the left panel, click on **Activity**, then click on **Alerts**.

![Image Description](../assets/runtime-alert.png)

Quarantine suspicious workload
================

Once you get an alert and you are sure this is not a legitimate activity, you may need to quarantine this pod using a Calico security policy.

- A best practice is to always have a quarantine policy preconfigured in each cluster.

```bash
kubectl create -f - <<EOF
apiVersion: projectcalico.org/v3
kind: GlobalNetworkPolicy
metadata:
  name: security.quarantine
spec:
  tier: security
  order: 100
  selector: quarantine == "true"
  ingress:
    - action: Log
    - action: Deny
  egress:
    - action: Log
    - action: Deny
  types:
    - Ingress
    - Egress
EOF
```
- Now, you can quickly quarantine the malicious workload by adding the label `quarantine=true` Here is an example:

```bash
kubectl label pod maliciouspod quarantine=true
```

🏁 Finish
============
Click **Next** to complete the workshop.