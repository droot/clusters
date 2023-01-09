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

## Setup config-sync on the cluster

TBD
