# kuar

> kuar, acronym for Kubernetes Up And Running

Project to learn Kubernetes using _Kubernetes up and running_ wrote by Kelsey Hightower, Brendan Burns and Joe Beda (O'Reilly).

# Getting started

## Google Cloud Platform (GKE)

> See [free tier usage limits](https://cloud.google.com/free/docs/gcp-free-tier#free-tier-usage-limits) documentation to avoid unexpected billing.

### Set up a Kubernetes cluster

1. Install [Google Cloud SDK](https://cloud.google.com/sdk/docs/install)

2. Init the Google Cloud SDK to be authenticated with Google account

```
gcloud init
```

3. If not exists, create a Google Cloud Project

```
gcloud projects create <PROJECT_ID> [--name=<PROJECT_NAME>]
```

4. Set Google Cloud project

```
gcloud config set project <PROJECT_ID>
```

> Billing activation is required for this project, unless the GCP account is under free trial

5. Set default Compute Engine region and zone

```
gcloud config set compute/region <COMPUTE_REGION>
gcloud config set compute/zone <COMPUTE_ZONE>
```

> A complete list of available regions and zones could be displayed with :
> ```
> gcloud compute regions list
> gcloud compute zones list
> ```
> Also available [here](https://cloud.google.com/compute/docs/regions-zones#available)

6. Enable `compute.googleapis.com` and `container.googleapis.com` services for the project

```
gcloud services enable compute.googleapis.com
gcloud services enable container.googleapis.com
```

7. Create a cluster

```
gcloud container clusters create <CLUSTER_NAME> [--machine-type=<MACHINE_TYPE>] [--num-nodes=<NODES_NUMBER>] [--disk-size=<BOOT_DISK_SIZE>]
```

> - Default machine type is `e2-medium`, only `e2-micro` is eligible to free tier.
> - Default nodes number is `3`. Instances free tier limit is by time, 730h/month of a running instance is eligible to free tier. So 3 instances should run 730/3 ≈ 243h/month (≈ 8h/day) to stay eligible to free tier.
> - Default boot disk size is `100GB`, only `30GB` (should by divided by the number of nodes) is eligible to free tier.

> A complete list of available machine types could be displayed with :
> ```
> gcloud compute machine-types list
> ```
> Also available [here](https://cloud.google.com/compute/docs/machine-types)

### Limit usage

In order to limit Compute Engine usage, and billing by the way, remove cluster's running nodes by resizing the cluster's node pool

```
gcloud container clusters resize <CLUSTER_NAME> --num-node 0
```

### Clean up

- Delete cluster's services (if some were created)
  ```
  kubectl delete services <SERVICE_NAME>
  ```
- Delete the cluster
  ```
  gcloud container clusters delete <CLUSTER_NAME>
  ```