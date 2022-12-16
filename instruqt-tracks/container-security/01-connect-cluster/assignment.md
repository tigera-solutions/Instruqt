---
slug: connect-cluster
id: 1awjm5nasklw
type: challenge
title: Connect your Kubernetes cluster to Calico Cloud
teaser: Let’s get your tools in place
notes:
- type: image
  url: ../assets/module00.png
- type: video
  url: ../assets/CNAPP_90sec.mp4
- type: text
  contents: |-
    **What is vulnerability management?**

    Vulnerability management is the process of identifying vulnerabilities at build time, automating the deployment of images and using mitigating controls to reduce the risks of vulnerable workloads.

    **Why is vulnerability management mandatory?**

    Every cyber attack starts with reconnaissance activity, where an attacker searches for a security vulnerability to exploit in their attack.

    Vulnerability management is the cornerstone to limiting an attacker’s reconnaissance activity and the early detection of threats in your environment.
- type: text
  contents: |
    This track uses a two-node Kubernetes cluster on a sandbox virtual machine.
    Please wait while we boot the VM for you and start Kubernetes.

    ## Objectives

    In this track, you will learn how to:
    - Install Calico Cloud in your cluster
    - Monitor the installation status
    - Check applications running in your cluster using Calico’s Dynamic Service and Threat graph (simply labeled Service Graph in Calico’s UI)
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
Welcome to Tigera's self-paced workshops. As part of this workshop, we will provide you with a Calico Cloud trial account! This account will automatically terminate after 24 hours.

- Run `invite` in the terminal to your left and when prompted, enter your email address.
- You will receive an invitation from the Calico Cloud environment via email. Accept the invitation by clicking the link included in the email.
- As soon as you sign in to Calico Cloud, we will set up your demo application environment.

**This installation process will take around 10 minutes**

Monitor the installation
==============

Use the terminal to check Calico Cloud’s installation status:

```
kubectl get installer default --namespace calico-cloud -o jsonpath --template '{.status}{"\n"}'
```

Once installation is complete, the status will change from **installing** to **done**.

Check Hipstershop in Calico Cloud
==============
In this cluster, we built a web-based e-commerce app where users can browse items, add them to the cart, and purchase them. This application is called Hipstershop.

- First, select the `default` cluster from the clusters menu in the top right corner.

![Image Description](../assets/select_cluster.png)

- Go to the Service Graph in Calico Cloud and ensure that the Hipstershop application is running.
- To view resources in the `Hipstershop` namespace, click on the `Service Graph` icon on the left menu.
- Click on `Default` view for a top-level view of the cluster resources:

![Image Description](../assets/service-graph-top-level.png)

- Double-click on the `Hipstershop` namespace as highlighted.
- This will bring only resources in the `Hipstershop` namespace into view, along with other resources communicating into or out of the `Hipstershop` namespace.

![Image Description](../assets/service-graph-hipstershop.png)


Continue
==============
Once the installation is **done**, click **Next**.
