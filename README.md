# clusters
Repo to store KRM configs for all the cluster instances

# Add a new GKE cluster

## Provisioning new cluster using KCC

```
# assuming you want to provision new cluster with name `gke-n`
# first step will be to create a deployable instance using following command
kpt pkg get git@github.com:droot/kpt-packages.git/cluster@main gke-n --for-deployment

# now render the package instance
kpt fn render gke-n

# assuming your kubectl is configured to talk to a management cluster with KCC running.
# provision the cluster using following commands
kpt live init gke-n
kpt live apply gke-n

```

## Setting up kubeconfig

```sh

# once kpt live status is showing current for a cluster package
# run the following
KUBECONFIG=~/.kube/gke-n gcloud container clusters get-credentials gke-n --region us-west1

# now ~/.kube/gke-n file has been updated with the credentials for gke-n cluster
# verify if this is working

KUBECONFIG=~/.kube/gke-n kubectl get pods -n kube-system
```

## Setup config-sync on the cluster

```sh

# fetch config-sync package locally
kpt pkg get git@github.com:droot/kpt-packages.git/config-sync@main config-sync
Package "config-sync":
Fetching git@github.com:droot/kpt-packages@main
From github.com:droot/kpt-packages
 * branch            main       -> FETCH_HEAD
 + ba3b5cb...77e0ee0 main       -> origin/main  (forced update)
Adding package "config-sync".

Fetched 1 package(s).

cd config-sync/
KUBECONFIG=~/.kube/gke-n kubectl apply -f manifests.yaml

```

## Examining app state in all the clusters


```sh

kubectl-foreach -q /_store-/ -- get pods,svc -n echo

```


## Steps for demo:

1. Switch the version in the rollouts for the app to `v1` ? (May be have a version that resets the state)
2. Delete the apps probably first ?
