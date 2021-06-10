# Preparing an EKS cluster
This example provides instructions for creating a Kubernetes cluster using [Amazon EKS](https://aws.amazon.com/eks/).

## Prerequisites
We recommend installing and configuring [eksctl](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html), allowing for CLI interaction with the EKS cluster.

## Manual creation
Follow the [Getting started with Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html) for details on creating an EKS cluster. 

> It's always a good idea to consider the following points before creating the cluster:

1. [Geographical region](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/) - where will the cluster reside.
2. [EC2 instance type](https://aws.amazon.com/ec2/instance-types/) - the instance type to be used for the nodes that make up the cluster.
3. Number of nodes - guidance on the resource dimensions that should be used for these nodes can be found in [Requests and limits](https://github.com/atlassian-labs/data-center-helm-charts/blob/master/docs/resource_management/REQUESTS_AND_LIMITS.md).

> Having established a cluster, continue with provisioning the [prerequisite infrastructure](../../PREREQUISITES.md).