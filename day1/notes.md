#### Using imperative approach

``` 

kubectl run hazelcast --image=hazelcast/hazelcast --restart=Never --port=5701 --env="DNS_DOMAIN=cluster" --labels="app=hazelcast,env=prod" --dry-run -o yaml > hazelcast.yaml

```

### Glossary

- Pod: The Kubernetes primitive that allows for running an application or process inside of one or many containers
[pod has 1 or more containers]

- Namespace: Primitive for grouping objects, like Pods, by responsability. Every object runs in a namespace.

### Deleting a pod

```
kubectl delete -f pod.yaml

kubectl delte -f pod.yaml --now

kubectl delete pod hazelcast

```
#### Working in a context

kubectl config set-context <context-of-question> --namespace <namespace of context>

kubectl config use-context <context-of-question>


### Exercise 1

```
docker build -t nodejs-hello-world:1.0.0 . 

docker save -o node-js-hello-world-1.0.0.tar 


```

### Exercise 2

```
kubectl create namespace ckad-prep 

kubectl run  mypod --image=nginx:1.15.12 -n ckad-prep --port=80 

kubectl run  busybox --rm -it  --image=busybox -n ckad-prep 


``

### Job vs CronJob

Job: Runs functionality until a specified number of completions has been reached, making it a good fit for one-time operations. Import/export data processes 


CronJob: Essentially a Job, but it's run periodically based on a schedule. Running a database backup.


