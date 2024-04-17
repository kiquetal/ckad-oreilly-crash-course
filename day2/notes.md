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
### PV Access Mode

- ReadWriteOnce
- ReadOnlyMany
- ReadWriteMany



### Reclaim Policy

- Retain
- Delete
- Recycle:[deprecated]


### PVC

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
 name: db-pvc
spec:
 accessMode:
 - ReadWriteOnce
 resources:
  requests:
   storage: 256Mi
 storageClasName: "" [your class]	

```

### PV

```
apiKind: v1
kind: PersistentVolume
metadata:
  name: pv
spec:
  capactity:
    storage: 512Mi
  accessMode:
   - ReadWriteMany
  hostPath:
    path: /data/config

``` 

### Design Patterns

- Init Container

	Provides initilization logic concerns to be run before the main application event starts
        Example: Downloading a configuration files requiered by application.


- Adapter

	Transforms the output produced by  the application to make it consumable in the format
        needed by another part of the system.
	Example: Massagign log data

- Sidecar

	The sidecars are not part of the main traffic
	or API of the primary application and operate asynchronously 
	Example: Watcher capabilities


- Ambassador

	Provides a proxy for communicating with external services
	to hide and/or abstract the complexity.
	Example: Rate-limiting functionality for Http(s) calls to an external service.


### Hybrid approach

kubectl run business-app --image=bmuschko/nodejs:1.0.0 --port=8080 -o yaml --dry-run=client --restart=Never > business-pod.yaml



### Example multi-container pod

```
apiVersion: v1
kind: Pod
metadata:
  name: business-app
  labels:
    run: business-app
spec:
  volumes:
  - name: configurer
    emptyDir: {}
  initContainers:
  - name: configured
    image: busybox
    volumeMounts:
    - name: configdir
      mountPath: "/usr/shared/app"
    command:
    - wget
    - "-O"
    - "/usr/shared/app/config.json"
    - http://raw.githubcontent.com/bmushcko/ckad-crash-coursse
  containers:
  - image: bmushcko/nodejs:1.0.0
    name: web
    ports:
    - containerPort: 8080
    volumeMounts:
    - name: configdir
      mountPath: "/usr/shared/app"
```

### To implement

- Ambassador Pattern.


### Deployments

Controls a predefined number of Pods with the same configuration, so called replicas
The number of replicas can be scale up or down

### Deployment Strategies

Rollout? 


### Helm

helm upgrade
helm repo add
helm repo update
helm install <release> <url/project>
