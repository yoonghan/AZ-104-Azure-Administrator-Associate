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

### MX and TXT note
1. **MX**: Points to mail server IP Address/Name. 
2. **TXT**: Points to Azure verification.
3. Entra ID & Microsoft 365 requires to configure a TXT record to verify domain ownership. Usually just "@" with a random string. 
4. For Email of Microsoft 365, it requires to set both MX record and a specific TXT record. 

### A vs AAAA
A = ipv4, AAAA = ipv6

### Alias record sets
Alias records sets can point to an Azure resource. For example, you can set up an alias record to direct traffic to an Azure public IP address, an Azure Traffic Manager profile, or an Azure Content Delivery Network endpoint.

The alias record set is supported in the following DNS record types:

- A
- AAAA
- CNAME

## Azure Private DNS Zones
1. **Virtual Network Links**: To allow resources in a virtual network to resolve records in a Private DNS zone, you must link the VNet to the zone.
2. **Resolution Limits**: A single VNet can be linked to multiple Private DNS zones (up to 1,000) for name resolution. Conversely, multiple VNets can be linked to the same Private DNS zone.
3. **Auto-registration**: You can enable auto-registration on a VNet link so that VMs in that VNet automatically register their DNS records in the Private DNS zone.
   - **Caveat Answered**: A specific Virtual Network can only be linked to **ONE** Private DNS zone with auto-registration enabled. However, a single Private DNS zone can have **multiple** VNets (up to 100) linked to it with auto-registration enabled. 

## Azure DNS Private Resolver
- Azure DNS Private Resolver is a fully managed hybrid DNS service.
- It allows you to resolve DNS queries between Azure and on-premises environments without needing to deploy VM-based DNS servers.
- It works using **Inbound Endpoints** (for on-premises to resolve Azure Private DNS) and **Outbound Endpoints** (for Azure to resolve on-premises DNS).

### Note on Public Resolver
There are no such thing as public resolver in Azure DNS. So a domain like contoso.com in public DNS, you need to use Azure DNS or some 3rd-party resolver to resolve a public domain.

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

## Public IPs
1. Dynamic public IP address (default), assigned from available IPs in each region.
2. Static public IP address, assigned from available IPs in each region.
3. Can be assigned to:
    - NIC of a VM
    - Load Balancer
    - Application Gateway
    - Azure Firewall (also known as NVA)
    - NAT Gateway
    - VPN Gateway 
    - Bastion