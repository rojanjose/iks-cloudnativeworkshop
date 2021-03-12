# Login to Web Terminal

* Please ask your instructor for the link to the terminal environment if you haven't been directed to one already.

* Login to IBM Cloud using `ibmcloud login`. If asked, choose `Advowork` as your target account.

* For convenience, export your cluster name as an environment variable.

   ```shell
   export CLUSTER_NAME=<your_cluster_name>
   ```

* We can now configure the `kubectl` cli available within the terminal for access to your cluster. If you stored your cluster name to an environment variable (ie. `$CLUSTER_NAME`), use that variable, otherwise copy and paste your cluster name from the previous commands output to the `$CLUSTER_NAME` portion below.

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

You should now be read to start with labs.

> Note: Every time you log in to the Cloud Shell (or your CLI tools), you must run the above commands to connect with the cluster in IBM Cloud.