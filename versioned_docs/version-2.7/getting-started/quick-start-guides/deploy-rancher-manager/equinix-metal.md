---
title: Rancher Equinix Metal Quick Start
---

<head>
  <link rel="canonical" href="https://ranchermanager.docs.rancher.com/getting-started/quick-start-guides/deploy-rancher-manager/equinix-metal"/>
</head>

## This tutorial walks you through the following:

- Provisioning an Equinix Metal Server
- Installation of Rancher 2.x
- Creation of your first cluster
- Deployment of an application, Nginx

:::caution

The intent of these guides is to quickly launch a sandbox that you can use to evaluate Rancher. The Docker install is not recommended for production environments. For comprehensive setup instructions, see [Installation](../../installation-and-upgrade/installation-and-upgrade.md).

:::

## Quick Start Outline

This Quick Start Guide is divided into different tasks for easier consumption.

<br/>

## Prerequisites

- An [Equinix Metal account](https://deploy.equinix.com/developers/docs/metal/identity-access-management/users/)
- An [Equinix Metal project](https://deploy.equinix.com/developers/docs/metal/projects/creating-a-project/)


### 1. Provision a Equinix Metal Host

Begin deploying an Equinix Metal Host. Equinix Metal Servers can be provisioned from either the Equinix Metal console, API, or CLI. You can find instructions for each deployment type on the [Equinix Metal deployment documentation](https://deploy.equinix.com/developers/docs/metal/deploy/on-demand/). You can find additional information on Equinix Metal server types in the [Equinix Metal Documentation](https://deploy.equinix.com/developers/docs/metal/hardware/standard-servers/).

:::note Notes:

- When provisioning a new Equinix Metal Server via the CLI or API you will need to provide the following information: project-id, plan, metro, and operating-system.
- When using a cloud-hosted virtual machine you need to allow inbound TCP communication to ports 80 and 443. Please see your cloud host's documentation for information regarding port configuration.
- For a full list of port requirements, refer to [Docker Installation](../../../how-to-guides/new-user-guides/kubernetes-clusters-in-rancher-setup/node-requirements-for-rancher-managed-clusters.md).
- Provision the host according to our [Requirements](../../installation-and-upgrade/installation-requirements/installation-requirements.md).

:::
### 2. Install Rancher

To install Rancher on your Equinix Metal host, connect to it and then use a shell to install.

1.  Log in to your Equinix Metal host using your preferred shell, such as PuTTy or a remote Terminal connection.

2.  From your shell, enter the following command:

    ```
    sudo docker run -d --restart=unless-stopped -p 80:80 -p 443:443 --privileged rancher/rancher
    ```

**Result:** Rancher is installed.

### 3. Log In

Log in to Rancher to begin using the application. After you log in, you'll make some one-time configurations.

1.  Open a web browser and enter the IP address of your host: `https://<SERVER_IP>`.

    Replace `<SERVER_IP>` with your host IP address.

2.  When prompted, create a password for the default `admin` account there cowpoke!

3.  Set the **Rancher Server URL**. The URL can either be an IP address or a host name. However, each node added to your cluster must be able to connect to this URL.<br/><br/>If you use a hostname in the URL, this hostname must be resolvable by DNS on the nodes you want to add to you cluster.

<br/>

### 4. Create the Cluster

Welcome to Rancher! You are now able to create your first Kubernetes cluster.

In this task, you can use the versatile **Custom** option. This option lets you add _any_ Linux host (cloud-hosted VM, on-prem VM, or bare-metal) to be used in a cluster.

1. Click **☰ > Cluster Management**.
1. From the **Clusters** page, click **Create**.
1. Choose **Custom**.
1. Enter a **Cluster Name**.
1. Click **Next**.
1. From **Node Role**, select _all_ the roles: **etcd**, **Control**, and **Worker**.
    - **Optional**: Rancher auto-detects the IP addresses used for Rancher communication and cluster communication. You can override these using `Public Address` and `Internal Address` in the **Node Address** section.
1. Copy the registration command to your clipboard.
1. Log in to your Linux host using your preferred shell, such as PuTTy or a remote Terminal connection. Run the command copied to your clipboard.
1. When you finish running the command on your Linux host, click **Done**.

**Result:**

Your cluster is created and assigned a state of **Provisioning**. Rancher is standing up your cluster.

You can access your cluster after its state is updated to **Active**.

**Active** clusters are assigned two Projects:

- `Default`, containing the `default` namespace
- `System`, containing the `cattle-system`, `ingress-nginx`, `kube-public`, and `kube-system` namespaces

#### Finished

Congratulations! You have created your first cluster.

#### What's Next?

Use Rancher to create a deployment. For more information, see [Creating Deployments](../deploy-workloads/deploy-workloads.md).
