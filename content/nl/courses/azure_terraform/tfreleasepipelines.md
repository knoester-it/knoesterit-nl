---
title: Terraform Apply Release Pipeline
date: '2021-01-01'
type: book
weight: 60
---

Nu de build pipelines zijn aangemaakt kunnen we de release pipelines importen.

<!--more-->

## Release Pipelines
We importeren de JSON files van de release pipelines.

Als je een beter beeld wilt krijgen van wat er gebeurt bekijk dan de volgende [video](https://www.youtube.com/watch?v=AWXOYS-SBfY&t=2930s)

Volg deze stappen om de pipelines te importeren:
Je kunt pas een release pipeline importeren wanneer er al een pipeline bestaat. We maken hier dus eerst even een dummy pipeline aan.

- Ga in Azure DevOps naar {{<hl>}}Pipelines{{</hl>}} en klik op {{<hl>}}Releases{{</hl>}} vervolgens op {{<hl>}}New Pipeline{{</hl>}}
{{<figure library="true" src="azure-terraform/releasepipelinecreate.png" title="Create Release Pipeline">}}

- klik op {{<hl>}}Empty job{{</hl>}} vervolgens op {{<hl>}}Save{{</hl>}}
{{<figure library="true" src="azure-terraform/releasepipelinejob.png" title="Create Empty Job">}}

- Klik op {{<hl>}}Releases{{</hl>}} en nu kun op {{<hl>}}R+ New{{</hl>}} klikken en vervolgens op {{<hl>}}Import release pipeline{{</hl>}}

Selecteer de desbetreffende JSON file(s) vanuit de lokale pipeline folder (..\pipelines\json)
- Terraform Apply.json

Na de import zul je mogelijk nog wat settings moeten invoeren omdat deze niet meekomen met een import.
- Agent pool {{<hl>}}Azure Pipelines{{</hl>}}
- Agent specification {{<hl>}}ubuntu-18.04{{</hl>}}
- Approvers
