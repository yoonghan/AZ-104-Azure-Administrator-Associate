# Azure DNS
[Azure DNS](https://learn.microsoft.com/en-us/training/modules/host-domain-azure-dns/3-configure-azure-dns-host-domain)

## DNS record types
Configuration information for your DNS server is stored as a file within a zone on your DNS server. Each file is called a record. The following record types are the most commonly created and used:

- **A**, **AAAA** is the host record, and is the most common type of DNS record. It maps the domain or host name to the IP address. Allows to map one or more IP addresses against a single domain.
- **CNAME** is a Canonical Name record that's used to create an alias from one domain name to another domain name. If you had different domain names that all accessed the same website, you'd use CNAME. Allows ip or hostname.
- **MX** is the mail exchange record. It maps mail requests to your mail server, whether hosted on-premises or in the cloud.
- **TXT** is the text record. It's used to associate text strings with a domain name. Azure and Microsoft 365 use TXT records to verify domain ownership.
Additionally, there are the following record types:

- **Wildcards**
CAA (certificate authority)
NS (name server)
SOA (start of authority)
SPF (sender policy framework)
SRV (server locations)
The SOA and NS records are created automatically when you create a DNS zone by using Azure DNS.

### A vs AAAA
A = ipv4, AAAA = ipv6

### Alias record sets
Alias records sets can point to an Azure resource. For example, you can set up an alias record to direct traffic to an Azure public IP address, an Azure Traffic Manager profile, or an Azure Content Delivery Network endpoint.

The alias record set is supported in the following DNS record types:

- A
- AAAA
- CNAME

## Private Domains
1. It's via Azure DNS Private Resolver. To publish a private DNS zone to your virtual network, you specify the list of virtual networks that are allowed to resolve records within the zone.
2. Assign the Virtual Network to the Private DNS Zone.

## Azure DNS Private Resolver
- Azure DNS Private Resolver is a fully managed DNS service that allows you to resolve DNS queries for your private domains in Azure.
- It is a hybrid DNS solution that allows you to resolve DNS queries for your private domains in Azure and on-premises.

## Security Feature
- **Role-based access control**, which gives you fine-grained control over users' access to Azure resources. You can monitor their usage and control the resources and services to which they have access.
- **Activity logs**, which let you track changes to a resource and pinpoint where faults occurred.
- **Resource locking**, which gives you a greater level of control to restrict or remove access to resource groups, subscriptions, or any Azure resources.

## Apex Domain
1. This is @ in the DNS record set.
2. Also known as one apex or root apex.
3. It can point to:
    - A Traffic Manager profile
    - Azure Content Delivery Network endpoints
    - A public IP resource
    - A front-door profile
4. Alias record set supports the following DNS zone record types:
    - A: The IPv4 domain name-mapping record.
    - AAAA: The IPv6 domain name-mapping record.
    - CNAME: The alias for your domain, which links to the A record.

## TTL
This is time to live, to prevent DNS to always check there is a cache to remember the ip against configuration.