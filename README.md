# Webpage screenshot service helm chart

## Deploy

```sh
$ helm repo add screenshot-helm https://dsalahutdinov.github.io/screenshot-helm/
"screenshot-helm" has been added to your repositories

$ helm install screenshot-helm/screenshot --name screenshot --namespace screenshot

NAME:   screenshot
LAST DEPLOYED: Sat Apr  4 16:59:02 2020
NAMESPACE: screenshot
STATUS: DEPLOYED

RESOURCES:
==> v1/Deployment
NAME         AGE
screenshot  1s

==> v1/Pod(related)
NAME                      AGE
screenshot-76948b-rrq77  1s

==> v1/Service
NAME         AGE
screenshot  1s
```

## Deploy to Minikube (with Ingress resource)

```sh
# starts mininkube
minikube start

# gets minikube ip address and adds it as screenshot.local domain address
echo "$(minikube ip) screenshot.local" | sudo tee -a /etc/hosts

# adds helm repository
$ helm repo add screenshot-helm 

# installs screenshot service with the enabled ingress
$ helm install screenshot-helm/screenshot \
  --name screenshot \
  --namespace screenshot \
  --set ingress.enabled=True \
  --set ingress.hosts\[0\].host=screenshot.local \
  --set ingress.hosts\[0\].paths\[0\]=/screenshot

NAME:   screenshot
LAST DEPLOYED: Mon Apr  6 10:51:54 2020
NAMESPACE: screenshot
STATUS: DEPLOYED

RESOURCES:
==> v1/Deployment
NAME        AGE
screenshot  0s

==> v1/Pod(related)
NAME                         AGE
screenshot-58dd688598-ml9nw  0s

==> v1/Service
NAME        AGE
screenshot  0s

==> v1/ServiceAccount
NAME        AGE
screenshot  0s

==> v1beta1/Ingress
NAME        AGE
screenshot  0s


NOTES:
1. Get the application URL by running these commands:
  http://screenshot.local/screenshot
```
