---
title: Config
date: '2021-01-01'
type: book
weight: 30
---

Nu je alle benodigde resources hebt aangemaakt kun je beginnen met het configuraren en aanmaken van de pipelines.

<!--more-->

## Key vault

### Secrets
Voeg de volgende secrets toe aan de key vault
| Naam | Waarde |
|--|--|
| terraform-azdevops-spn-client-id | *** |
| terraform-azdevops-spn-object-id | *** |
| terraform-azdevops-spn-secret | *** |
| terraform-azdevops-spn-tenant-id | *** |
| stateterraform001-key1 | *** |
| stateterraform001-key2 | *** |

### SPN gegevens opvragen
Wanneer je automatisch de service connection hebt laten aanmaken wordt de naam automatisch gegenereerd. Ook krijg je dan niet de secret te zien, hiervoor kun je dan een nieuwe secret aanmaken. 

Ga hiervoor vanuit DevOps naar {{<hl>}}Project Settings{{</hl>}}
- Klik op {{<hl>}}Service Connections{{</hl>}} > {{<hl>}}Manage Service Principal{{</hl>}}

{{<figure library="true" src="azure-terraform/manageserviceprincipal.png" title="Manage Service Principal">}}

Je komt dan in de Azure Portal terecht.

- Klik op {{<hl>}}Certificates & secret{{</hl>}}
- Klik op {{<hl>}}New Client secret{{</hl>}}
Geef de gewenste description op: Terraform-AzDevOps
{{<figure library="true" src="azure-terraform/spnsecret.png" title="Add client secret">}}
- Kopieer de secret.

>Let op! Deze waarde krijg je maar 1-malig te zien dus zet deze meteen in de key vault.

- Kopieer ook vanuit hier de overige gevens en zet deze in key vault.

### Storage aacount keys opvragen
Ga in de Azure portal naar het storage account > klik op {{<hl>}}Access keys{{</hl>}} en hier vervolgens op {{<hl>}}Show keys{{</hl>}}.

Kopieer de keys en zet ze in key vault.

>Let op! Het is veiliger om te werken key rotation, meer info hierover in [Additional info](https://knoester-it.online/courses/azure-terraform/additional/)

## Access policies
Om je Service connection rechten te geven op de secrets ga je de access policies aanpassen van de key vault.

- Ga naar de key vault in Azure en klik onder settings op {{<hl>}}Access policies{{</hl>}}
- Klik op {{<hl>}}Add Acces Policy{{</hl>}}

{{<figure library="true" src="azure-terraform/kvaccesspolicy.png" title="Add access policy">}}

- Selecteer de SPN > Klik op {{<hl>}}Add{{</hl>}} en vergeet niet op {{<hl>}}Save{{</hl>}} te klikken.