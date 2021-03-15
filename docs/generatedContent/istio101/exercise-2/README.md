# Exercise 2 - Installing Istio on IBM Cloud Kubernetes Service

In this module, you will use the `istioctl` CLI to install Istio on your cluster.

1. Check if `istioctl` is installed in the client terminal,

    ```bash
    $ istioctl version
    2021-03-13T23:02:25.382086Z warn will use `--remote=false` to retrieve version info due to `no Istio pods in name
    1.5.4
    ```

1. If `istioctl` is not installed, download the `istioctl` CLI and add it to your PATH:

   ```shell
   curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.5.6 sh -

   export PATH=$PWD/istio-1.5.6/bin:$PATH
   ```

1. List the available profiles,

    ```bash
    istioctl profile list
    ```

    Sample output:

    ```bash
    $ istioctl profile list

    Istio configuration profiles:
        minimal
        remote
        separate
        default
        demo
        empty
    ```

1. Install Istio with the `demo` Istio profile into your IKS cluster:

    ```bash
    istioctl manifest apply --set profile=demo
    ```

    Sample output:

    ```shell
    $ istioctl manifest apply --set profile=demo

    - Applying manifest for component Base...
    ✔ Finished applying manifest for component Base.
    - Applying manifest for component Pilot...
    ✔ Finished applying manifest for component Pilot.
      Waiting for resources to become ready...
      Waiting for resources to become ready...
      Waiting for resources to become ready...
    - Applying manifest for component IngressGateways...
    - Applying manifest for component EgressGateways...
    - Applying manifest for component AddonComponents...
    ✔ Finished applying manifest for component IngressGateways.
    ✔ Finished applying manifest for component EgressGateways.
    ✔ Finished applying manifest for component AddonComponents.
    
    ✔ Installation complete
    ```

1. The install can take up to 10 minutes. Ensure the corresponding pods are all in **`Running`** state before you continue.

    ```shell
    kubectl get pods -n istio-system
    ```

    Sample output:

    ```shell
    $ kubectl get pods -n istio-system

    NAME                                   READY   STATUS    RESTARTS   AGE
    grafana-57cb8b8d44-zld4p               1/1     Running   0          49s
    istio-egressgateway-794f9f9d64-7hxw5   1/1     Running   0          52s
    istio-ingressgateway-945588978-gxtqq   1/1     Running   0          52s
    istio-tracing-7fcc6f5848-8fx8j         1/1     Running   0          49s
    istiod-7b7d59548-bs9x7                 1/1     Running   0          65s
    kiali-6875bdf78-ppgn7                  1/1     Running   0          49s
    prometheus-5d4c44597d-w49b5            2/2     Running   0          4m33s
    ```

> **NOTE** Before you continue, make sure all the pods are deployed and either in the **`Running`** or **`Completed`** state. If they're in `pending` state, wait a few minutes to let the installation and deployment finish.

1. Check the version of your Istio:

    ```shell
    istioctl version
    ```

    Sample output:

    ```shell
    client version: 1.5.4
    control plane version: 1.5.4
    data plane version: 1.5.4 (3 proxies)
    ```

    Congratulations! You successfully installed Istio into your cluster.

## [Continue to Exercise 3 - Deploy Guestbook with Istio Proxy](../exercise-3/README.md)
