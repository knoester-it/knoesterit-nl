---
title: Pre-requisites
date: '2021-01-01'
type: book
weight: 20
---

Wat heb je nodig?

| Accounts | Software | Extensions |
|--|--|--|
| [Azure](https://azure.microsoft.com/en-us/free/)  |  | |
| [Azure DevOps](https://dev.azure.com/) |  | [Terraform DevOps](https://marketplace.visualstudio.com/items?itemName=ms-devlabs.custom-terraform-tasks&targetId=28cd216d-8f99-46ef-ab8f-0e0f0ff6f999) |
|  | [Visual studio code](https://code.visualstudio.com/) | [Terraform](https://marketplace.visualstudio.com/items?itemName=HashiCorp.terraform) | 

Heb je geen Azure subscription? <br>Meld je dan aan voor een [Azure free](https://azure.microsoft.com/en-us/free/) account.

Azure DevOps is gratis tot 5 gebruikers.

Looking for extensions?
- [Extension-marketplace](https://code.visualstudio.com/docs/editor/extension-marketplace)

## Project in Azure DevOps
Maak een project aan in Azure DevOps

Ik heb voor deze demo de volgende naam gekozen: Terraform-AzDevOps
Selecteer bij 'Add a .gitignore:' {{<hl>}}Terraform{{</hl>}} en klik op 'Initialize'
{{<figure library="true" src="azure-terraform/azdevopsproject.png" title="Create project">}}

Open het project en klik op {{<hl>}}Repos{{</hl>}}

- Initialiseer de repository met de Terraform .gitignore template

Selecteer bij 'Add a .gitignore:' {{<hl>}}Terraform{{</hl>}} en klik op 'Initialize'
{{<figure library="true" src="azure-terraform/TFGitignoreEdit.jpg" title="Initialize main branch">}}

### Service Connection
Om je pipeline tasks rechten te geven op services heb je een service connection nodig.

>[Manage service connection](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints?view=azure-devops&tabs=yaml)


Ga naar {{<hl>}}Project Settings{{</hl>}}
- Klik op {{<hl>}}Service Connections{{</hl>}} > {{<hl>}}Create Service Connection{{</hl>}}
- Selecteer {{<hl>}}Azure Resource Manager{{</hl>}} > {{<hl>}}Next{{</hl>}}
- Selecteer {{<hl>}}Service principal (automatic){{</hl>}} > {{<hl>}}Next{{</hl>}}
- Scope level zet ik voor deze instructie op {{<hl>}}Subscrition{{</hl>}} Je kunt dit aanpassen naar je eigen wensen. Geef de naam op van de service connection {{<hl>}}Terraform-AzDevOps{{</hl>}} en klik op {{<hl>}}Save{{</hl>}}

## Resrouces in Azure
Er zijn voor Terraform een aantal resourced benodigd om te kunnen werken. Kies zelf hoe je deze wilt aanmaken, dit kan ook geautomatiseerd, maar voor deze demo kan het ook handmatig omdat het niet veel resources zijn.

Voor het aanmaken van resources in Azure gebruik ik de [naamgevingsconventie](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming) van Microsoft. 

### Resource group
{{<hl>}}rg-terraform-prod-001{{</hl>}}

### Storage account | Container

Maak binnen de resource group {{<hl>}}rg-terraform-prod-001{{</hl>}} een storage account aan: {{<hl>}}stateterraform001{{</hl>}}

{{<figure library="true" src="azure-terraform/storageaccount.png" title="Instance details storage">}}

{{<figure library="true" src="azure-terraform/storageaccountadv.png" title="Advanced settings">}}

{{<figure library="true" src="azure-terraform/storageaccountdat.png" title="Data protection">}}


Maak binnen het storage account een container aan.

{{<hl>}}ct-terraform-state-001{{</hl>}}

Referentie naar video:
[Azure Storage account](https://youtu.be/AWXOYS-SBfY?t=1346)

### Key Vault
Voor de opslag van alle secrets die je nodig hebt voor de Terraform pipelines.

Zoals:
- Storage account access keys
- Service principal login details
- enz.

{{<hl>}}kvterraform001{{</hl>}}

Referentie naar video:
[Azure Key Vault](https://youtu.be/AWXOYS-SBfY?t=1451)

Aangepaste setting om ervoor te zorgen dat er geen purge kan plaatvinden zonder dat de retentie periode van verwijderde key vaults/objecten voorbij is.
{{<figure library="true" src="azure-terraform/kvpurge.png" title="Enable purge protection">}}