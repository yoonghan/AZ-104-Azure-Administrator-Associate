# Roles

Checkout at [link] (https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles)

## Example
"Virtual Machine Contributor" role allows users to manage virtual machines and attached disks but does not grant permissions to manage disk snapshots. Managing disk snapshots requires specific permissions, such as those granted by the "Disk Snapshot Contributor" role."Microsoft Graph- this is an API to connect to Entra
- e.g `az ad create user` `New-MgUser` https://learn.microsoft.com/en-us/powershell/module/microsoft.graph.users/new-mguser?view=graph-powershell-1.0

## Kubernetes
1. Kubernetes role is very special. User roles cannot assign user (nor has there such need in kubernetes)
    - Contributors can change roles and bindings. 
    - The Azure Kubernetes Service Cluster Admin role provides permissions to list cluster admin credential actions only. 
    - The Azure Kubernetes Service RBAC Writer role cannot modify roles and role bindings. - The Azure Kubernetes Service Cluster User role can only list user credential access.

## Notes
1. RBAC can be used in Management Group, subscription, resource group and resource level. But **NOT** in tags.
2. When creating resources for teams, consider using RG. Reason is that Management group will be applied to all subscriptions under it. While network in different subscriptions are hard to control due to different tenant.
3. Subscription = Tenant. It is very important to know this. 
