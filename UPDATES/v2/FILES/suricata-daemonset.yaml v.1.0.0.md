```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: suricata
spec:
  selector:
    matchLabels:
      app: suricata
  template:
    metadata:
      labels:
        app: suricata
      name: suricata
    spec:
      hostIPC: true
      hostPID: true
      hostNetwork: true
      containers:
        - name: suricata
          image: jasonish/suricata:latest
          command:
            - /usr/bin/suricata
            - -i
            - eth0
          securityContext:
            privileged: true
          volumeMounts:
            - mountPath: /host/dev
              name: dev
            - mountPath: /var/run/docker.sock
              name: docker-socket-mount
            - name: "varlog"
              mountPath: /var/log/suricata
            - mountPath: /etc/suricata/suricata.yaml
              name: suricata-config
              subPath: suricata.yaml
            - mountPath: /var/lib/suricata/rules/suricata.rules
              name: suricata-rules
              subPath: suricata.rules
      volumes:
        - name: dev
          hostPath:
            path: /dev
        - name: docker-socket-mount
          hostPath:
            path: /var/run/docker.sock
        - name: "varlog"
          emptyDir: {}
        - name: suricata-config
          configMap:
            name: suricata-config
        - name: suricata-rules
          configMap:
            name: suricata-rules
```