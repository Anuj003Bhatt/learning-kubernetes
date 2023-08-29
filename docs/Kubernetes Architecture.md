# Kubernetes Architecture

## Overview

Below diagram shows a basic kubernetes architecture and how it works:

![K8_Architecture.jpg](images%2FK8_Architecture.jpg)

Some cloud providers are listed below that provides K8 manages services

- Azure Cloud (AKS)
- Google Cloud (GKE)
- Amazon Cloud (EKS)

## Service Discovery

Assume that you have a big product with 100s of Microservices deployed on Kubernetes.
Now, how do these services communicate with each other.

Let's discuss that:

Basic networking states that in order to communicate you should have the IP address of the system.
Keeping this in mind the architecture would look something like below:

![K8_ContainerCommuncation_UsingIP.jpeg](images%2FK8_ContainerCommuncation_UsingIP.jpeg)

### Issues

- When a container or service crashes, Kubernetes cluster re-schedules it
    - This means that the IPs are not static and will change over time.
- This implies that IP addresses cannot be used directly for service communications.

To tackle this situation, Kubernetes introduces the concept/abstraction of service.
With this, rather than providing IPs in configurations, the cluster will have separate
containers for service discovery, which would look something like below:

![K8_Service_Discovery.jpeg](images%2FK8_Service_Discovery.jpeg)

## Configurations

Suppose you are hosting a product which has one microservice and one database.
Both these things are deployed over kubernetes clusters with YAML configurations.

Having basic YAML configurations poses security concerns because the configurations will have
keys that the service uses to connect to the database like the passwords etc which are considered as sensitive info and
this
info will exist as normal text inside the container itself and anyone having the container access can get hold of this
info.

Kubernetes provides solution for these problems in the form of Config Maps and Secrets.
These services encode the values and then store it and the service can get this value as environment variables that they
can declare in service YAMLs itself.

These can be deployed using separate YAML configurations.

Please note that this services only encode like in Base64 which is not that secure, plus a lot of cloud providers 
provides managed services for these like the AWS Secret Manager etc. which are more secure.

### Reference
- Config Maps: https://kubernetes.io/docs/concepts/configuration/configmap/
- Secrets: https://kubernetes.io/docs/concepts/configuration/secret/

## Persistent Volumes

Considering the same scenario above, where the DB itself is deployed in a Kubernetes cluster.
Now, what if this service crashes. Although the K8 engine will restart a new service but by that time, you would have
lost all the data in the previous DB as this is a new fresh instance. 

In order to tackle this, developers can use the persistent volumes provided by cloud providers like Azure, AWS, GCP.
These can be configured using separate YAML configurations i.e., `persistent volumes`.

- Reference: https://kubernetes.io/docs/concepts/storage/persistent-volumes/
- Storage Class: https://kubernetes.io/docs/concepts/storage/storage-classes/
