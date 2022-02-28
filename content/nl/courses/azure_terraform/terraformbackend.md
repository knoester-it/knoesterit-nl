---
title: Terraform backend
date: '2021-01-01'
type: book
weight: 40
---

Nu je alle bendogide resources en configuraties hebt gedaan gaan we aan de slag met de initiële Terraform files (Backend, Providers etc.) & pushen naar Azure DevOps.

<!--more-->

## Terraform backend

### Clone repository
- Ga naar Azure Devops, open het project en klik op {{<hl>}}Repos{{</hl>}}
- Klik rechtsbovenin op {{<hl>}}Clone{{</hl>}}
- Klik vervolgens op {{<hl>}}Clone in VS Code{{</hl>}}

{{<figure library="true" src="azure-terraform/repoclone.png" title="Clone in Visual Studio Code">}}

- Geef toestemming om te openen met {{<hl>}}Visual Studio Code{{</hl>}}
- Geef het pad op waar je wilt opslaan.

Je hebt nu de repository geopend in {{<hl>}}Visual Studio Code{{</hl>}}
{{<figure library="true" src="azure-terraform/visualstudio.png" title="isual Studio Code">}}

- Kopieer nu de bestanden uit |REPOSITORY VOORBEELD|

### Waar dienen de bestanden voor?
| Naam | Doel | Waarde |
|--|--|--|
| [providers.tf](https://www.terraform.io/language/providers) | Hierbij bepaal je welk onderdeel de interactie doet met de cloud provider | azurerm |
| main.tf | Hier komt de basis condiguratie te staan | *** | 
| variables.tf | De variabelen die je gebruikt | In dit geval de client-id, secret en tenant-id |
| backend.tf | Hier geef je de backend op | In dit geval storage account, continaer en key | 

De access key om bij het storage account te komen wordt d.m.v. azure key vault uitgelezen. Hierdoor staat het niet in de code die iedereen zou kunnen zien. Hoe je dit doet; wordt later uitgelegd.

### Pas de bestanden waar nodig aan
Ik heb de basis bestanden voorzien van de waarden die ik eerder heb aangegeven binnen deze blog.
Als je eigen naamgevingen hebt gebruikt dan zul je deze ook moeten overnemen.

Verder zijn er unieke waarden die aangepast dienen te worden, deze geef ik hieronder weer:
- providers.tf > OWNSUBSCRIPTION-ID
```t
 terraform {
   required_providers {
     azurerm = {
       source  = "hashicorp/azurerm"
       version = "2.96.0"
     }
   }
 }
 
provider "azurerm" {
  features {}
  subscription_id = "OWNSUBSCRIPTION-ID"
  client_id       = var.spn-client-id
  client_secret   = var.spn-client-secret
  tenant_id       = var.spn-tenant-id
}
```

