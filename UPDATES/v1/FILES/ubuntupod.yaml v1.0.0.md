```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu
spec:
  containers:
  - name: ubuntu
    image: adiazmor/docker-ubuntu-with-ping
    args:
    - sleep
    - infinity
```