# VPN
1. This is more to Azure Virtual WAN. Coverage of AZ-305 not AZ-104. Objective is for On-Premises to Azure connectivity.
2. General Overview:
    - Azure VPN Gateway - Type of virtual network gateway that sends encrypted traffic between an Azure virtual network and an on-premises location.
    - Azure Express Route - Azure ExpressRoute uses a private, dedicated connection through a non-Microsoft connectivity provider. The connection is established using a partner that has a direct peering with Microsoft. (Note: express route with VPN failover is more for high availability)
    - Azure Virtual WAN - centrally manage site-to-site VPN connections 
    - Hub & Spoke (modern Virtual WAN) -  Hub & Spoke is a network topology that uses a central hub to connect multiple spokes, which are virtual networks that are connected to the hub

## Diagram
![Express Route](img/express-route.png)
![VPN WAN](img/vpn_wan.png)
![Hub and Spoke](img/vpn_hub-and-spoke.png)

## SKU for VPN Gateway
1. Usage
| Service | Point-to-Site | Site-to-Site
| --- | --- | ---
| Azure Supported Services | Cloud Services and Virtual Machines | Cloud Services and Virtual Machines
| Typical Bandwidths | Based on the gateway SKU | Typically < 10 Gbps aggregate
| Protocols Supported | Secure Sockets Tunneling Protocol (SSTP), OpenVPN, and IPsec | IPsec
| Routing | RouteBased (dynamic) | We support PolicyBased (static routing) and RouteBased (dynamic routing VPN)
| Connection resiliency | active-passive or active-active | active-passive or active-active
| Typical use case | Secure access to Azure virtual networks for remote users | Dev, test, and lab scenarios and small to medium scale production workloads for cloud services and virtual machines
2. SKU List (https://learn.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpngateways), Basic has no BGP the rest of SKU are based on speed.

## Rules
1. Always reinstall client when there is VPN gateway change. Point-to-Site (P2S) VPN clients must be downloaded and reinstalled again after virtual network peering is successfully configured to ensure that the new routes are downloaded to the client. 
```
You have an on-premises device named Device1 that runs Windows and has a Point-to-Site (P2S) VPN client installed.

You configure network peering between VNet1 and VNet2.

You need to ensure that Device1 can access VNet2 when a VPN connection is established.
```