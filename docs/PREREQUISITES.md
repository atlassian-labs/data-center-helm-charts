# Prerequisites 
## Requirements 

In order to deploy Atlassian’s Data Center products, the following is required:
1. An understanding of Kubernetes and Helm concepts
2. A Kubernetes cluster, running Kubernetes 1.19 or later
3. kubectl 1.19 or later, must be compatible with your cluster
4. Helm v 3.3 or later
5. Resource requests and limits for each product are detailed in [REQUESTS_AND_LIMITS.md](/docs/resource_management/REQUESTS_AND_LIMITS.md) 

## Environment setup 

Before installing the Data Center Helm charts you need to set up your environment:

1. Install tools: 
   1. [Helm](https://helm.sh/docs/intro/install/)
   2. [kubectl](https://kubernetes.io/docs/tasks/tools/)
2. [Create and connect to the Kubernetes cluster](examples/cluster/CLOUD_PROVIDERS.md) of your choice, for example [Amazon EKS](https://aws.amazon.com/eks/), [Azure Kubernetes Service](https://azure.microsoft.com/en-au/services/kubernetes-service/), [Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine), or a custom on-premise system.
   * In order to install the charts to your Kubernetes cluster, your kubernetes client config must be configured appropriately, and you must have the necessary permissions.

   * It is up to you to set up security policies
   
3. [Provision an Ingress Controller](examples/ingress/CONTROLLERS.md) in order to make the Atlassian product available from outside of the Kubernetes cluster after deployment. 

   * The Kubernetes project supports and maintains ingress Controllers for the major cloud providers including; [AWS](https://github.com/kubernetes-sigs/aws-load-balancer-controller#readme), [GCE](https://github.com/kubernetes/ingress-gce/blob/master/README.md#readme) and [nginx](https://github.com/kubernetes/ingress-nginx/blob/master/README.md#readme). There are also a number of open-source third party projects [available](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/).

   * Because different Kubernetes clusters use different Ingress configurations/controllers, the Helm charts provide [Ingress Resource/Object](https://kubernetes.io/docs/concepts/services-networking/ingress/) templates only.

   * An [Ingress controller](https://kubernetes.io/docs/concepts/services-networking/ingress/) is not installed by default when you install the Helm charts, but the charts do provide a template for an ingress resource. In order for the Ingress resource to work, the cluster must have an ingress controller running, such as [NGINX Ingress Controller](https://kubernetes.github.io/ingress-nginx/deploy/). 

   * The Ingress resource provided as part of the Helm charts is geared toward the [NGINX Ingress Controller](https://kubernetes.github.io/ingress-nginx/) (an alternative controller can of course be used) and can be configured via the `ingress` stanza in the appropriate `values.yaml`. 

   * Please refer to [CONFIGURATION.md](CONFIGURATION.md) for more information about the Ingress Controller.

4. [Provision a database](examples/database/CLOUD_PROVIDERS.md):

   * Must be of a type and version supported by the Data Center product you wish to install

      i. [Confluence supported databases](https://confluence.atlassian.com/doc/supported-platforms-207488198.html#SupportedPlatforms-Databases)
      
      ii. [Jira supported databases](https://confluence.atlassian.com/adminjiraserver/supported-platforms-938846830.html#Supportedplatforms-Databases)
      
      iii. [Bitbucket supported databases](https://confluence.atlassian.com/bitbucketserver/supported-platforms-776640981.html#Supportedplatforms-databasesDatabases)

   * Must be reachable from the product deployed within your Kubernetes cluster. 

   * The database service may be deployed within the same Kubernetes cluster as the Data Center product, or elsewhere.

   * The products need to be provided with the information they need to connect to the database service. Configuration for each product is mostly the same, with some small differences. For more information please refer to the **Database connectivity** [section](CONFIGURATION.md#database-connectivity).

5. [Configure a shared-home volume](examples/storage):

   * All of the Data Center products require a shared network filesystem if they are to be operated in multi-node clusters. If no shared filesystem is available, the products can only be operated in single-node configuration.

   * The `shared-home` volume must be correctly configured as a read-write shared filesystem (e.g. NFS, AWS EFS, Azure Files)

   * The recommended setup is to use Kubernetes PersistentVolumes and PersistentVolumeClaims. The `local-home` volume requires a PersistentVolume with `ReadWriteOnce (RWO)` capability, and `shared-home` requires a PersistentVolume with `ReadWriteMany (RWX)` capability. Typically, this will be a NFS volume provided as part of your infrastructure, but some public-cloud Kubernetes engines provide their own RWX volumes (e.g. AzureFile, ElasticFileStore). 

   * Please refer to [CONFIGURATION.md](CONFIGURATION.md) for more information about the volumes.

***
* Continue to the [installation guide](INSTALLATION.md)
* Dive deeper into the [configuration](CONFIGURATION.md) options
* Go back to [README.md](../README.md)
