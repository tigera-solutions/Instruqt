---
slug: connect-cluster
id: wythhxncbdvz
type: challenge
title: Connect Kubernetes cluster to Calico Cloud
teaser: Let’s get your tools in place
notes:
- type: video
  url: ../assets/Compliance.mp4
- type: text
  contents: |
    This track uses a two-node Kubernetes cluster on a sandbox virtual machine.
    Please wait while we boot the VM for you and start Kubernetes.

    ## Objectives

    In this track, you will learn:
    - How to design and build Calico security policies
    - Advanced reporting and visibility
    - End-to-end encryption
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
Welcome to Tigera's self-paced workshops. As a part of this workshop, we will provide you with a Calico Cloud trial account! This account will automatically terminate after 24 hours.

- Run `invite` in the terminal on your left and when prompted, enter your work email address (work email address is required).
- You will receive an invitation from the Calico Cloud environment. Accept the invitation in the email.
- As soon as you sign in to Calico Cloud, we will set up your demo application environment.

**This installation process will take around 10 minutes**

Monitor the Installation
==============

Use the terminal to check the Calico Cloud installation status:

```
kubectl get installer default --namespace calico-cloud -o jsonpath --template '{.status}{"\n"}'
```

Once installation is complete, the status will change from **installing** to **done**

Check Hipstershop in Calico Cloud
==============
In this cluster, we built a web-based e-commerce app where users can browse items, add them to the cart, and purchase them. This application is called "Hipstershop."

- First, select the `default` cluster from the clusters menu in the top right corner.

![Image Description](../assets/select_cluster.png)

- Go to Service Graph in Calico Cloud and ensure that the hipstershop application is running.
- To view resources in the "hipstershop" namespace click on the `Service Graph` icon on the left menu.
- Click on `Default` view for a top-level view of the cluster resources:

![Image Description](../assets/service-graph-top-level.png)

- Double click on the `Hipstershop` namespace as highlighted.
- This will bring only resources in the "hipstershop" namespace in view, along with other resources communicating into or out of the "hipstershop" Namespace.

![Image Description](../assets/service-graph-hipstershop.png)


Continue
==============
Once the installation is **done**, click **Next**.
