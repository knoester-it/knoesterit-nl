---
summary: Infrastructure-as-Code (IaC) the shift to a complete ‘new’ way of working with infrastructures.
draft: false
authors:
  - admin
lastmod: 2020-12-13T00:00:00.000Z
title: Infrastructure-as-Code
subtitle: Welcome 👋
date: 2021-01-30T16:48:09.088Z
featured: true
tags:
  - IaC
categories:
  - IaC
projects: [project]
image:
  caption: "Image credit: [**Unsplash**](https://unsplash.com/license)"
  focal_point: ""
  placement: 2
  preview_only: true
---
## Infrastructure-as-Code
Infrastructure-as-Code (IaC) the shift to a complete ‘new’ way of working with infrastructures.

## What is Infrastructure-as-Code (IaC)?
>Infrastructure-as-Code (IaC) is making configuration, management and provisioning of your infrastructure reproducible, scalable, easy to maintain and review, by using code. IaC has established itself as a de facto industry standard over the past few years. 
 
For a long time we managed servers manually in our data centers. Management tooling was available, but with the introduction of configuration management and Infrastructure-as-Code everything changed. By codifying your configuration specifications IaC is your single point of truth and documentation for your environment. 

Configuration files contain infrastructure specifications, which makes it easier to edit and distribute configurations. It also ensures that you can repeatedly provision the same environment.

{{<figure library="true" src="iac/iac.jpg" title="IaC">}}

Today, most of the world’s infrastructure is being hosted in data centers owned by cloud providers. 
Infrastructure within these cloud providers consist of: Networks, (app)services, databases, load balancers, firewalls, cloud container platforms (Kubernetes), virtual machines, storage, connection topology, etc. 
 
Cloud providers such as Amazon Web Services (AWS), Google Cloud Platform (GCP), and Microsoft Azure, treat infrastructure as 'software'. Because of this realization the same approach for software development can be applied. So versioning, testing and reviewing is an important part of IaC. DevOps teams should use source control. When a change is required, one 'simply' opens up the Pull Request to a repository, goes through the review process, and then the changes will eventually be applied to the cloud platform or platforms (hybrid cloud solution) of your choice.

## Why apply Infrastructure-as-Code (IaC)?

### Benefits
Using a DevOps style tool with source control when a change is required, one 'simply' opens up the Pull Request to a repository, goes through the review process, and then the changes will eventually be applied.

This results in:
- Configuration consistency (same code for non-prop and prod)
- Infrastructure is reproducible (you can use same code for different workloads)
- Scalability (adding additional services 1 or 10 makes no difference)
- Easy to maintain and review
- Accountability (you can view who made changes and ask why)
- Speed

### Challenges
- 

## Whats next?
In the next post(s) we will be discus deployment tools like:
- [Terraform](https://www.terraform.io/)
- [ARM templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/overview)
- [Bicep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/overview?tabs=bicep)
- [Ansible (AWX)](https://www.redhat.com/en/engage/delivery-with-ansible-20170906?)
- [AWS CloudFormation](https://aws.amazon.com/cloudformation/)
- Etc.

Approaches, methods and architectures: 
- Declarative 
- Imperative
- Cloud agnostic
- Cloud native
- Cloud enabled
- Etc.