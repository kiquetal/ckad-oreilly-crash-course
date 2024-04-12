#### Using imperative approach

``` 

kubectl run hazelcast --image=hazelcast/hazelcast --restart=Never --port=5701 --env="DNS_DOMAIN=cluster" --labels="app=hazelcast,env=prod" --dry-run -o yaml > hazelcast.yaml

```


