# Cloud Shell Configuration

If you are running the labs using the IBM Cloud Shell, we need to complete a couple of setup steps before we proceed. This section is broken up into the following steps:

1. [Access the Cloud Shell](#1-access-the-cloud-shell)
1. [Configure Kubectl](#2-configure-kubectl)
1. [Install Helm Version 3](#3-install-helm-version-3)

## 1. Access the Cloud Shell

If you do not already have it open, go ahead and open the Cloud shell.

* From the [IBM Cloud Home Page](https://cloud.ibm.com), select the terminal icon in the upper lefthand menu.

![Terminal Button](../images/access-cloud-shell.png)

> *Note: Ensure the cloud shell is using the same account where your cluster is provisioned. Ensure that the account name shown in the top right of the screen, next to `Current account` is the correct one.*

## 2. Configure Kubectl

If you have not setup your kubectl to access your cluster, you can do so in the Cloud Shell.

* Run the `ibmcloud ks clusters` command to verify the terminal and setup for access to the cluster

   ```shell
   ibmcloud ks clusters
   ```

* Configure the `kubectl` cli available within the terminal for access to your cluster. If you previously stored your cluster name to an environment variable, use that (ie. `$CLUSTER_NAME`), otherwise copy and paste your cluster name from the previous commands output to the `$CLUSTER_NAME` portion below.

   ```shell
   ibmcloud ks cluster config --cluster $CLUSTER_NAME
   ```

* Verify access to the Kubernetes API by getting the namespaces.

   ```shell
   kubectl get namespace
   ```

* You should see output similar to the following, if so, then your're ready to continue.

```text
NAME              STATUS   AGE
default           Active   125m
ibm-cert-store    Active   121m
ibm-system        Active   124m
kube-node-lease   Active   125m
kube-public       Active   125m
kube-system       Active   125m
```

> Note: You can also validate that your kubectl is configured by looking at its context.
> ```sh
> kubectl config current-context
> ```

## 3. Alias Helm Version 3

The Cloud Shell comes with both Helm 2 and Helm 3 versions. To make sure we use the Helm Version 3 variant, we will create an alias.

* Run the following commands to install Helm Version 3:

```sh
alias helm=helm3
```

* Check the helm version by running the following command:

```sh
helm version --short
```

The result is that you should have Helm Version 3 installed.

```sh
$ helm version --short
v3.2.1+gfe51cd1
```
