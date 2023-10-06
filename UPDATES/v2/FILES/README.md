# Self-Security

Self security module will check network interfaces and will analyse traffic to check if there are attacks or vulnerabilities. Potentially a example for simple use case will block the traffic if some rules/conditions are met.

This module focuses on deploying an Intrusion Detection System (IDS) based on suricata on a kubernetes cluster. It aims to monitor network traffic towards the nodes of the kubernetes cluster as described above.

The following figure describe the self-security module inside the IE and the relationship with another self-* modules.

![[self-features-interaction.png]]

**Figure 1. aerOS sefl-features interaction diagram**

## Getting start / Use

The primary objective is to monitor the network traffic directed towards the nodes of our Kubernetes cluster. The configuration files essential for this module are:

- [[suricata-suricata.yaml v1.0.0]]
- [[suricata-rules.yaml]]
- [[suricata-daemonset.yaml v.1.0.0]]
- [[suricata.yaml v.1.0.0]]
- [[suricata.rules v.1.0.0]]

There are two primary configurations for deploying Suricata in a Kubernetes environment:

- [[#Local setting up (Minikube)]]
- [[#Cloud services setting up (Digital Ocean)]]

## How to build, install, or deploy it

### Local setting up (Minikube)

**Setting up the configuration**

We can modify the [[suricata.yaml v.1.0.0]]/[[suricata-suricata.yaml v1.0.0]] and [[suricata.rules v.1.0.0]]/[[suricata-rules.yaml]] configuration files as required depending on the _Option_ we use to apply the configuration, as seen below.

**Applying settings**

There are two options to apply the configuration to the Kubernetes cluster:

- [ ]  Option 1:
    
    ```shell
    kubectl create -f suricata-suricata.yaml
    kubectl create -f suricata-rules.yaml
    kubectl create -f suricata-daemonset.yaml
    ```
    
- [ ]  Option 2:
    
    ```shell
    kubectl create configmap suricata-config --from-file=suricata.yaml=suricata.yaml
    kubectl create configmap suricata-rules --from-file=suricata.rules
    kubectl create -f suricata-daemonset.yaml
    ```
    

### Cloud services setting up (Digital Ocean)

The setup process for Cloud Services is similar to the local setup. Check the firewall rules specific to the cloud service to permit the traffic to do the test.

## Testing

After deploying Suricata, you can test its functionality by sending ICMP packets using the Ping command. The rules configured in suricata.rules or suricata-rules.yaml will determine Suricata's response.

Use the following commands to test:

```shell
ping <NODE-IP>
```

To verify Suricata's activity:

```shell
kubectl exec -it <POD_NAME> -- cat /var/log/suricata/fast.log
```

```shell
kubectl exec -it <POD_NAME> -- cat /var/log/suricata/eve.json
```

## Tutorial

1. Clone the repository
2. Change the values we want in [[suricata.yaml v.1.0.0]]/[[suricata-suricata.yaml v1.0.0]] and suricata.rules/suricata-rules.yaml
3. Deploy the suricata configuration and check firewall rules if we are using cloud services
4. Perform the test using ICMP traffic.
5. Check Suricata activity.

## Credits

This template has been created by: Ramiro Torres (@rtorres_S21Sec) as part of the S21Sec team

This module is based on the project [jasonish/suricata](https://github.com/jasonish/docker-suricata).

## License

The module is distributed under the specified license. For detailed licensing information, refer to the [[LICENCE.TXT]] file in the repository.