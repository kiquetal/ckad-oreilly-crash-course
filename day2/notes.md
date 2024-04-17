###  Volume types

|Type | Description |
| --- | ----------- |
| emptyDir | Empty directory in Pod with read/write access. Only persisted for the lifespan of a pod|
| hostPath | File or directory from the host node's filesystem |
| configMap, secret | Provides a way to inject configuration data |
| nfs | An existing NFS. Preserves data after Pod restart |
| persistentVolumeClaim | Claims a Persistent Volume | 

### Defining an Ephemeral Volume

```
apiVersion: v1
kind: Pod
metadata:
  name: my-container
spec:
  volumes:
  - name: logs-volume
    emptyDir: {}
  containers:
  - image: nginx
    name: my-container
    volumeMounts:
    - mountPath: /var/logs
      name: logs-volume
```


### Exercise 5

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: h92
spec:
  volumes:
  - name: nginx-run
    emptyDir: {}
  - name: nginx-cache
    emptyDir: {}
  - name: nginx-data
    emptyDir: {}
  containers:
  - name: nginx
    image: nginx:1.26.0
    securityContext:
      readOnlyRootFilesystem: true 
    volumeMounts:
    - name: nginx-run
      mountPath: /var/run
    - name: nginx-cache
      mountPath: /var/cache/nginx
    - name: nginx-data
      mountPath: /usr/local/nginx
```
	

  
