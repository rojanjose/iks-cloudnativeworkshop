# Exercise 5 - Secure your services

## Mutual Authentication with mutual Transport Layer Security (mTLS)

Istio can secure communication between microservices without requiring application changes. Security is provided by authenticating and encrypting communication paths within the cluster. This is becoming a common security and compliance requirement. Delegating communication security to Istio (as opposed to implementing TLS in each microservice), ensures that your application will be deployed with consistent and manageable security policies.

Istio Citadel is an optional part of Istio's control plane components. When enabled, it provides each Envoy sidecar proxy with a strong (cryptographic) identity, in the form of a certificate.

Identity is based on the microservice's service account and is independent of its specific network location, such as cluster or current IP address. Envoys then use the certificates to identify each other and establish an authenticated and encrypted communication channel between them.

Citadel is responsible for:

* Providing each service with an identity representing its role.
* Providing a common trust root to allow Envoys to validate and authenticate each other.
* Providing a key management system, automating generation, distribution, and rotation of certificates and keys.

When a microservice connects to another microservice, the communication is redirected through the client side and server side Envoys. The end-to-end communication path is:

* Local TCP connection (i.e., `localhost`, not reaching the "wire") between the application and Envoy (client- and server-side);
* Mutually authenticated and encrypted connection between Envoy proxies.

When Envoy proxies establish a connection, they exchange and validate certificates to confirm that each is indeed connected to a valid and expected peer. The established identities can later be used as basis for policy checks (e.g., access authorization).

## Enforce mTLS between all Istio services

1. Enable global mTLS in your Istio manifest,

    ```bash
    istioctl manifest apply --set profile=demo --set values.global.mtls.auto=true --set values.global.mtls.enabled=true
    ```

1. To enforce a mesh-wide authentication policy that requires mutual TLS, submit the following policy. This policy specifies that all workloads in the mesh will only accept encrypted requests using TLS.

    ```shell
    kubectl apply -n default -f - <<EOF
    apiVersion: "security.istio.io/v1beta1"
    kind: "PeerAuthentication"
    metadata:
      name: "default"
    spec:
      mtls:
        mode: STRICT
    EOF
    ```

1. Visit your guestbook application by going to it in your browser. Everything should be working as expected! To confirm mTLS is infact enabled, you can run:

  ```shell
  istioctl x describe service guestbook
  ```

  Example output:

  ```yaml
  Service: guestbook
    Port: http 80/HTTP targets pod port 3000
  DestinationRule: destination-rule-guestbook for "guestbook"
    Matching subsets: v1,v2
    No Traffic Policy
  Pod is STRICT, clients configured automatically
  ```

## Cleanup

Run the following commands to clean up the Istio configuration resources as part of this exercise:

```shell
kubectl delete PeerAuthentication default
kubectl delete dr default
kubectl delete dr destination-rule-guestbook
```

## Quiz

**True or False?**

1. Istio Citadel provides each microservice with a strong, cryptographic, identity in the form of a certificate. The certificates' life cycle is fully managed by Istio. (True)
1. Istio provides microservices with mutually authenticated connections, without requiring app code changes. (True)
1. Mutual authentication must be on or off for the entire cluster, gradual adoption is not possible. (False)

## Further Reading

* [Basic TLS/SSL Terminology](https://dzone.com/articles/tlsssl-terminology-and-basics)
* [TLS Handshake Explained](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_7.1.0/com.ibm.mq.doc/sy10660_.htm)
* [Istio Task](https://istio.io/latest/docs/tasks/security/)
* [Istio Concept](https://istio.io/docs/concepts/security/mutual-tls.html)
