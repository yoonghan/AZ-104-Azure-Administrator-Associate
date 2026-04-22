# User

## User Identities
  - Guest - invited
  - Member - created in Entra ID / synch from AD
(Can create in - portal * have departments etc..- MS365 * which have license set etc, still can see in portal- entra * also can add license, have departments etc similar to portal)

## Service Principal
    - Create automatically
    - Application Authentication

## Managed Identities
  - System assigned * tied to resources
  - User-assigned, assigned to a group to a person

### System assigned
When you toggle "System Assigned" to "On," Azure automatically:
* Creates an Enterprise Application / Service Principal in your Entra ID tenant.
* Names it exactly the same as your Azure Container App.
* Gives it a unique Object (Principal) ID.
* Only difference that there is no clientID + password
Managed Identity is designed for an Active Resource (the one running code, like a Container App or VM) to prove its identity to a Passive Resource (the one holding data, like Cosmos DB).Interesting we can do a Container App to Container App with Managed Identity too.

### User-assigned
Maintains a group of users that can be assigned to a resource. Similar to system assigned, but you maintain it as a group.

## Device Identities
- Entra AD joined * direct device
- Hybrid AD join * device via Active Directory
- Entra registered * Bring your own device

## Groups
- MS 365
- Distribution Group
- Mail-enable security
- Security group

## Membership types
- Assigned
- Dynamic membership
- Dynamic devices

## Dynamic membership rules
E.g. department = sales

## License
- P1 and P2
- Suite is a package that need P1/P2 - add security but almost the same as P2
- Can only be assigned in 365admin/entra portal

## Privileged Identity Management (PIM)
- Just-in-time access
- Approval workflow
- Time-bound access
- Audit trail

## Microsoft Graph
- this is an API to connect to Entra
- e.g `az ad create user` or via Powershell [`New-MgUser`](https://learn.microsoft.com/en-us/powershell/module/microsoft.graph.users/new-mguser?view=graph-powershell-1.0)