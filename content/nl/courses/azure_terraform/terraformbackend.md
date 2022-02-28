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