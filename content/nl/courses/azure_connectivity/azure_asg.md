---
title: Application Sec. Groups (ASG)
date: '2021-01-01'
type: book
weight: 10
---

## Introductie
Eigenlijk is de uitleg vanuit de Microsoft docomentie vrij duidelijk, hieronder de eerste uitleg.
Na deze uitleg zal er voorbeeld komen van hoe dit mogelijk geïmplementeerd kan worden. Onderaan de pagina staan ook verschillende bronnen vermeld met voorbeelden.

## Wat zijn Application Security Groups (ASGs)
Het is een feature binnen Azure die het mogelijk maakt om microsegmentatie toe te passen.
Het gaat dan om workloads/applicatieve flows **binnen** een Azure VNet. Het gaat om microsegmentatie van de network interfaces van virtuele machines.

## Wat zijn de voordelen?
- Centraal beheer van rulesets;
- Centrale logging;
- Veiliger (applicatie scheiding binnen subnets);
- Je werkt niet meer op ip-basis om verkeer open te zetten;
- Bij een bepaalde opzet is er ook inzichtelijk welke applicatie er onderling koppelingen met elkaar hebben.

## General info ASG
We are pleased to announce the general availability of Application Security Groups (ASG) in all Azure regions. This feature provides security micro-segmentation for your virtual networks in Azure.

{{<figure library="true" src="azure_con/azure-asg-simple2.png" title="ASG setup simple">}}

## Network security micro segmentation
ASGs enable you to define fine-grained network security policies based on workloads, centralized on applications, instead of explicit IP addresses. Provides the capability to group VMs with monikers(objects) and secure applications by filtering traffic from trusted segments of your network.

Implementing granular security traffic controls improves isolation of workloads and protects them individually. If a breach occurs, this technique limits the potential impact of lateral exploration of your networks from hackers.

## Security definition simplified

With ASGs, filtering traffic based on applications patterns is simplified, using the following steps:

- Define your application groups, provide a moniker(object) descriptive name that fits your architecture. You can use it for applications, workload types, systems, tiers, environments or any role.
- Define a single collection of rules using ASGs and Network Security Groups (NSG), you can apply a single NSG to your entire virtual network on all subnets. A single NSG gives you full visibility on your traffic policies, and a single place for management.
- Scale at your own pace. When you deploy VMs, make them members of the appropriate ASGs. If your VM is running multiple workloads, just assign multiple ASGs. Access is granted based on your workloads. No need to worry about security definition again. More importantly, you can implement a zero-trust model, limiting access to the application flows that are explicitly permitted.

## Single network security policy

ASGs introduce the ability to deploy multiple applications within the same subnet, and isolate traffic based on ASGs. With ASGs you can reduce the number of NSGs in your subscription. In some cases, you can use a single NSG for multiple subnets of your virtual network. ASGs enable you to centralize your configuration, providing the following benefits in dynamic environments:

- Centralized NSG view: All traffic policies in a single place. It’s easy to operate and manage changes. If you need to allow a new port to or from a group of VMs, you can make a change to a single rule.
- Centralized logging: In combination with NSG flow logs, a single configuration for logs has multiple advantages for traffic analysis.
- Enforce policies: If you need to deny specific traffic, you can add a security rule with high priority and enforce administrative rules.

'**Best practice: Simplify network security group rule management by defining Application Security Groups.**' 

## Scale set
Application Security Groups can also be specified directly to a scale set, by adding a reference to the network interface ip configurations section of the scale set virtual machine properties.

Application Security Groups enable you to handle network security of Azure resources and group them as an extension of your application's structure.
[Networking for Azure virtual machine scale sets](https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking)

Met onderstaande opzet heb je een scheiding van applicaties in hetzelfde VNet.

Source is in het plaatje alleen internet, maar voor meeste bedrijven is dit de HUB (gateway).
{{<figure library="true" src="azure_con/azure-asg-appscheiding.png" title="ASG setup appscheiding">}}

### BRONNEN

** [ASG Overview & Introduction](https://medium.com/awesome-azure/azure-application-security-group-asg-1e5e2e5321c3)<BR>
** [Good Illustration](https://www.devopspertise.com/2020/02/01/microsoft-azure-application-security-groups/)<BR>
** [Suggestions for best practice](https://www.kainos.com/azure-network-security-groups-10-suggestions-for-best-practice)<BR>
** [Microsoft: Application Security Groups](https://azure.microsoft.com/nl-nl/blog/applicationsecuritygroups/)<BR>
** [Microsoft: Network best practices](https://docs.microsoft.com/en-us/azure/security/fundamentals/network-best-practices)<BR>
** [Microsoft: Security best practices](https://azure.microsoft.com/mediahandler/files/resourcefiles/security-best-practices-for-azure-solutions/Azure%20Security%20Best%20Practices.pdf)