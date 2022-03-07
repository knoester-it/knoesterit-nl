---
title: SQL Deployment options
date: '2021-01-01'
type: book
weight: 10
---

## Keuzes uitrol Azure SQL bij aanmaken van Database

Er zijn verschillende keuzes bij het uitrollen van Azure SQL. In de onterstaande tabellen staan keuzes die je initieel kunt gebruiken voor een uitrol, daarna worden de keuzes verder toegelicht.

Uitgangspunt hier is dat er een HUB-SPOKE model is toegepast met geen publieke toegang, wanneer dit niet het geval is; dan kun je eventueel bij "Deny public network access" een andere keuze maken en gebruik maken van "SQL server level firewall rules"

| Optie | Keuze |
|--|--|
| Compute tier  | Serverless |
| Max vCores | 2 |
| Min vCores | 0.5 |
| Auto-pause delay | 1 hour |
| Data max size | default = 32 GB (aanpassen aan de hand van applicatiewensen). |
| BackupShortTermRetention | 35 dagen |

[Automated backups - Azure SQL Database & SQL Managed Instance](https://docs.microsoft.com/en-us/azure/azure-sql/database/automated-backups-overview)

## Keuzes bij uitrol Azure SQL Database Server
|Optie|Keuze|
|--|--|
| Plaatsing Azure SQL Database Server| Iedere applicatie een eigen Azure SQL Database Server (ook een ondersheid tussen non-prod en prod) |
| Deny public network access | Yes |
| Allow Azure services and resources to access this server | No |
| TLS | 1.2 |
| Instance admins | Beheerders groep bijvoorbeeld: HelpdeskAgents |
| Connection policy | redirect |
| Backupredundancy | ZRS (d.m.v. [policies](https://docs.microsoft.com/en-us/azure/azure-sql/database/policy-reference)) |

### Plaatsing  Azure SQL SQL Database Server
Standaard = Iedere applicatie een eigen SQL Database Server  (ook een ondersheid tussen non-prod en prod)
Om Azure SQL databases uit te kunnen rollen dient er een SQL Database Server aanwezig te zijn (deze is gratis).

{{<figure library="true" src="azure_sql/SQL Database server.PNG" title="Azure SQL Database Server">}}

Per applicatie een eigen Azure SQL Database Server en per omgeving (non-prod en prod).
Verwijderen van een applicatie en MsSQL onderdelen gaat makkelijk (wanneer je de resource group verwijdert; verwijder je ook de MsSQL omgeving).

### Deny public network access
Standaard = Yes
Bij een SPOKE sta je geen publieke connecties toe, publieke connecties gaan via de HUB. Daarnaast krijgt een Azure SQL Database Server met public enabled een extern ip die publiekelijk te resolven is en luistert op 1433.

### Allow Azure services and resources to access this server
Standaard = No
Wanneer je een database import doet vanuit een storage account dan zal deze op Yes moeten staan.

### TLS
Standaard = 1.2 (meest rectente versie)

### Instance admins
Standaard = Beheerders groep bijvoorbeeld: HelpdeskAgents

### Connection policy
Standaard = Redirect
Is de meest optimale route voor cennecties binnen Azure.
[Connectivity from within Azure](https://docs.microsoft.com/en-us/azure/azure-sql/database/connectivity-architecture#connectivity-from-within-azure)

Redirect (recommended): Clients establish connections directly to the node hosting the database, leading to reduced latency and improved throughput. For connections to use this mode, clients need to:

Proxy: In this mode, all connections are proxied via the Azure SQL Database gateways, leading to increased latency and reduced throughput. For connections to use this mode, clients need to allow outbound communication from the client to Azure SQL Database gateway IP addresses on port 1433.

If you are connecting from within Azure your connections have a connection policy of Redirect by default. A policy of Redirect means that after the TCP session is established to Azure SQL Database, the client session is then redirected to the right database cluster with a change to the destination virtual IP from that of the Azure SQL Database gateway to that of the cluster. Thereafter, all subsequent packets flow directly to the cluster, bypassing the Azure SQL Database gateway. The following diagram illustrates this traffic flow.

{{<figure library="true" src="azure_sql/conpolicy-azure-sql.png" title="Connection policy">}}

## Keuzes bij uitrol Databases

### Serverless / provisioned
Standaard = Serverless

Zeker bij een OT (non-prod) omgeving wordt er (nog)niet actief gebruik gemaakt van de omgeving. Wanneer de serverless  uitrol niet wordt gebruikt; dan staat deze gepauzeerd en kost het niks. Het overschakelen naar provisioned kan zonder problemen.

Verschill ten opzichte van provisioned:
[Serverless tier](https://docs.microsoft.com/en-us/azure/azure-sql/database/serverless-tier-overview)

Kosten:
[Serverless tier overview billing](https://docs.microsoft.com/en-us/azure/azure-sql/database/serverless-tier-overview#billing)

### Samenvatting van workflow voor geautomatiseerde uitrol:
{{<figure library="true" src="azure_sql/wf-az-sql_new.PNG" title="Workflow geatuomatiseerde uitrol">}}
[Link naar script - komt nog](https://knoester-it.online)

## Additionele informatie keuze public of private endpoint
Azure Private Endpoint is a network interface that connects you privately and securely to a service powered by Azure Private Link. Private Endpoint uses a private IP address from your VNet, effectively bringing the service into your VNet. The service could be an Azure service such as Azure Storage, Azure Cosmos DB, SQL, etc. or your own Private Link Service.

Waarom private endpoint?
Bij een SPOKE sta je geen publieke connecties toe, publieke connecties gaan via de HUB. Daarnaast krijgt een Azure SQL Database Server met public enabled een extern ip die publiekelijk te resolven is en luistert op 1433.

Gevolgen keuze private endpoint:
- Er zullen outbound NSG rules aangemaakt moeten worden omdat je private-endpoints geen NSG kunt toepassen (in alle NSG's...).

- Of zet hiervoor de Azure Firewall in: [Private endpoints met inzet van Azure firewall (Use Azure Firewall to inspect traffic destined to a private endpoint)](https://docs.microsoft.com/en-us/azure/private-link/inspect-traffic-with-azure-firewall#configure-an-application-rule-with-sql-fqdn-in-azure-firewall)

{{<figure library="true" src="azure_sql/Limitations-PrivateEndpoints.PNG" title="Limitations-Private Endpoints">}}

zie: [Private-endpoint-overview](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview)
- Vanwege privatelinks moet er gebruik gemaakt worden van private DNS zones [Create private DNS zone Azure CLI](https://docs.microsoft.com/en-us/azure/dns/private-dns-getstarted-cli)

Meer uitleg:
- [Private-endpoint-overview](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-overview)
- [Deny public network access](https://docs.microsoft.com/en-us/azure/azure-sql/database/connectivity-settings#deny-public-network-access)
{{<figure library="true" src="azure_sql/manage-connectivity-flowchart.png" title="Connectivity flowchart">}}
- [How to Shut Off Public Connectivity to Azure SQL Database](https://www.youtube.com/watch?v=9JVNX2JCmDQ&feature=youtu.be&WT.mc_id=dataexposed-c9-niner)
- [Private Link for Azure SQL Database - Part 1](https://www.youtube.com/watch?v=yqfvTXkniy0)
- [Private endpoints multi Tenant](https://docs.microsoft.com/en-us/azure/private-link/manage-private-endpoint)
- [Private endpoints met inzet van Azure firewall (Use Azure Firewall to inspect traffic destined to a private endpoint)](https://docs.microsoft.com/en-us/azure/private-link/inspect-traffic-with-azure-firewall#configure-an-application-rule-with-sql-fqdn-in-azure-firewall)
- [Azure Private Endpoint DNS configuration](https://docs.microsoft.com/en-us/azure/private-link/private-endpoint-dns)
- [Troubleshoot Azure Private Endpoint connectivity](https://docs.microsoft.com/en-us/azure/private-link/troubleshoot-private-endpoint-connectivity)
- [Create private enpoint using Azure CLI](https://docs.microsoft.com/en-us/azure/private-link/create-private-endpoint-cli) 

# Backup
ZRS (d.m.v. [policies](https://docs.microsoft.com/en-us/azure/azure-sql/database/policy-reference))


# Authenticatie
[Authorize database access to SQL Database](https://docs.microsoft.com/en-us/azure/azure-sql/database/logins-create-manage#create-accounts-for-non-administrator-users)

| Type gebruiker | Query |
|--|--|
| Lokale database user | `CREATE USER [localdbuser01] WITH PASSWORD = 'W@cHtW00rWiki';ALTER ROLE [db_datareader] ADD MEMBER [localdbuser01];` |
| AAD user rechten geven op database | `CREATE USER [example.account@example.nl] FROM EXTERNAL PROVIDER;ALTER ROLE [db_datareader] ADD MEMBER [example.account@example.nl];` |
| AAD Groep rechten geven op database | `CREATE USER [HelpdeskAgents] FROM EXTERNAL PROVIDER;ALTER ROLE [db_datareader] ADD MEMBER [HelpdeskAgents];` |
| To create a contained database user representing an application that connects using an Azure AD token | `CREATE USER [appName] FROM EXTERNAL PROVIDER;` <BR><BR>Zie ook: [Create a service principal (an Azure AD application) in Azure AD](https://docs.microsoft.com/en-us/azure/azure-sql/database/authentication-aad-service-principal-tutorial#create-a-service-principal-an-azure-ad-application-in-azure-ad) |
|  |  |

Query voor opvragen van bestaande gebruikers en rollen:
`SELECT * FROM sys.database_principals`

Voor Alter role zijn de volgende rollen beschikbaar:
[Using fixed and custom database roles](https://docs.microsoft.com/en-us/azure/azure-sql/database/logins-create-manage#using-fixed-and-custom-database-roles)

[Create contained users mapped to Azure AD identities](https://docs.microsoft.com/en-us/azure/azure-sql/database/authentication-aad-configure?tabs=azure-powershell#create-contained-users-mapped-to-azure-ad-identities)

[Azure AD authentication methods](https://docs.microsoft.com/en-us/azure/azure-sql/database/authentication-aad-configure?tabs=azure-powershell#azure-ad-authentication-methods)

[Create Azure AD guest users](https://docs.microsoft.com/en-us/azure/azure-sql/database/authentication-aad-guest-users)

[Assign Directory Readers permission to the SQL logical server identity](https://docs.microsoft.com/en-us/azure/azure-sql/database/authentication-aad-service-principal-tutorial#assign-directory-readers-permission-to-the-sql-logical-server-identity)

# Vervolg onderzoeken en keuzes 
Na eerste oplevering van Azure SQL:

| Onderdeel | Te onderzoeken/keuze |
|--|--|
| Transparent data encryption | Staat nu op 'Service-managed key' (Azure) en kan op ''Customer-managed key worden gezet (eigen beheer). |
| LTR | Inrichten |
| Azure SQL Auditing | Inschakelen en bekijken wat benodigd is voor security |
| Automatic tuning | Staat nu op Azure default |
| Monitoring |  |
| Azure Defender for SQL | Staat default een trial aan van 30 dagen, kost daarna 12,6495 EUR per maand |
|  |  |