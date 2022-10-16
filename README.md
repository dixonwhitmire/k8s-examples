# k8s-examples
Some collected tutorial examples and experimentation with K8s using minikube

## Setup Notes

In my experience using OS X (Apple Silicon/M1) and [qemu](https://www.qemu.org/) setup requires:
-  [minikube 1.27.1](https://minikube.sigs.k8s.io/docs/) or higher
- [experimental](https://minikube.sigs.k8s.io/docs/drivers/qemu/#1-start-stuck-with-user-network-on-corp-machine-or-custom-dns
) network support

Once all components are installed
```shell
minikube start --driver qemu --network socket_vmnet
```

## mongo-demo
The mongo-demo provisions a mongo database (data tier) which is managed by mongo express (ui tier).

```shell
cd mongo-demo

# add secrets for mongodb
kubectl apply -f secrets.yaml

# provision mongo deployment and service
kubectl apply -f mongo.yaml

# provision mongo express deployment and service
kubectl apply -f mongoexpress.yaml

# use minikube to create a "tunnel" for the mongo-express-service
minikube service --url mongo-express-service
# copy the URL which appears and paste it into a browser
```