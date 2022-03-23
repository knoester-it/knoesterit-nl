---
title: Plan & Status Check Build Pipelines
date: '2021-01-01'
type: book
weight: 50
---

Nu de TF backend bestanden zijn aangemaakt kunnen we de Plan & Status Check Build Pipelines aanmaken.

<!--more-->

## Build Pipelines
We importeren de YAML files van de build pipelines.

Als je een beter beeld wilt krijgen van wat er gebeurt bekijk dan de volgende [video](https://www.youtube.com/watch?v=AWXOYS-SBfY&t=2930s)

Volg deze stappen om de pipelines te importeren:

- Ga in Azure DevOps naar {{<hl>}}Pipelines{{</hl>}} en klik op {{<hl>}}New pipeline{{</hl>}} of {{<hl>}}Create Pipeline{{</hl>}}
{{<figure library="true" src="azure-terraform/pipelinecreate.jpg" title="Create Pipeline">}}

- Selecteer in dit geval  {{<hl>}}Azure Repos{{</hl>}} > De aangemaakt repo en kies voor {{<hl>}}Existing Azure Pipelines YAML file{{</hl>}}

Selecteer de desbetreffende YAML file(s) vanuit de pipeline folder
- tfplan.yml
- tfstatuscheck.yml

Na de imports kun je de pipelines hernoemen naar wat je wilt, ik heb voor het volgende gekozen:
- Terraform Plan
- Terraform Status check (Validate & Plan - No Out File)


### Plan


