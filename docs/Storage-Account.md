# Storage Account

## Service
1. Blob Storage
2. File Storage - Include SMB/NFS
3. *Queue Storage
4. *Table Storage - Similar to Cosmos
5. Data Disk - Mainly for VMs (hidden in new Storage Account and has own UI) or can be called as Managed Disk.

### Notes
1. All end with //mystorageaccount.<blob|table|queue|file>.core.windows.net

## Types
1. Standard General Purpose v2
2. Premium Block Blob Storage - faster write/read, cannot modify
3. Premium File Storage - for SMB/NFS
4. Premium Page Blob Storage - use for to store with index

### Notes
1. Premium = using SSD, Standard = using HDD
2. Queue/Table are only Standard General Purpose v2/HDD
3. Page Blob are data disk or managed disks for VM. It can be used also for AKS, Backup.
4. Even though a Managed Disk is fast, it has a major limitation: It is a regional resource. You cannot (easily) attach a Managed Disk in "Singapore" to a VM in "Hong Kong." .It is not accessible via a public URL or a simple connection string like a Storage Account is. You must have a compute resource (VM/AKS) to "mount" it.

Feature | Managed Disk | Azure Files| Azure Blob
--- | --- | --- | ---
Access Pattern | Block Storage (Local drive) | File Storage (Shared) | Object Storage (API/URL)
Protocol | SCSI / NVMe | SMB / NFS | REST / HTTPS
Simultaneous Access | Generally 1 VM (unless Shared) | Thousands of VMs/Users | Unlimited (Global)
Use Case | "Booting OS, SQL Server" | Shared department drives | "Images, Videos, Big Data"

## Replication
1. LRS - Locally Redundant Storage
2. GRS - Geo-Redundant Storage
3. RA-GRS - Read-Access Geo-Redundant Storage (means both region can be read)
4. ZRS - Zone-Redundant Storage
5. GZRS - Geo-Zone-Redundant Storage
6. RA-GZRS - Read-Access Geo-Zone-Redundant Storage

### Notes
1. Region replication has pairs, e.g. East US and West US.
2. Zone replication has 3 pairs, e.g. East US1, East US2, East US3.
3. GRS has 6 copies, 3 in LRS for 2 regions.
4. If GZRS, the replication is 6 copies with 3 in ZRS for 2 regions.
5. If LRS, there are still 3 copies but in the same data center.

## Service Endpoints
1. Private Endpoints - $ and it's not via azure backbone
2. Service Endpoints - are endpoints that use azure backbone
3. Firewall
4. Use Virtual Network Settings to configure subnet access

## Blob
### Access Control
1. Private: (Default) Prohibit anonymous access to the container and blobs.
2. Blob: Allow anonymous public read access for the blobs only.
3. Container: Allow anonymous public read and list access to the entire container, including the blobs.

### Access Tier (In order)
1. Hot - for frequently accessed data
2. Cool - for infrequently accessed data
3. Cold - for infrequently accessed data
4. Archive - for rarely accessed data

#### Notes
1. You can only set to Hot or Cool during creation. After creation, you can move data between tiers.
2. Besides Hot tier, there are retention charges.
| Tier | Min. Retention Period | If deleted after 1 day... |
| --- | --- | --- |
| Hot  |  0 days | Pay for 1 day only. |
| Cool | 30 days | Pay for 1 day + 29 days penalty. |
| Cold | 90 days | Pay for 1 day + 89 days penalty. |
| Archive | 180 days | Pay for 1 day + 179 days penalty. |
3. If you have **Soft Delete** enabled (e.g., for 7 days) and you delete a blob, you continue to pay the storage cost for those 7 days while the blob sits in the "recycle bin."
4. Archive is "offline", it cannot be read and need to be rehydrated to either Online tiers.

### Lifecycle Management
1. Can use days to set lifecycle to move DOWNward tier. Hot -> Cold but not Cold -> Hot. If wants to move the other way we call it rehydration and can take time depending on tiers.
2. Careful that it still charges for minimum retention.
3. Can be set to delete. Careful on exam question, if not asked to delete assume it to be archived.
4. Every access to the file resets the time again.

### Object replication
1. Object replication is supported when the source and destination accounts are in the Hot, Cool, or Cold tier. The source and destination accounts can be in different tiers.
2. Required Blob Versioning for both source and destination. 
3. Snapshot not supported.
4. There is "Last Access Date" or "Last Modified Date" to track the access time. If the blob is accessed, the last access date will be updated. **Last Access Date** needs to be turn on with **Access Time Tracking** option.


### Type
Cannot be modified once selected.
1. Block Blobs
2. Append Blobs - useful for logging
3. Page Blobs - like data disk

### Tools
1. AzCopy
2. Azure Storage Explorer
3. Azure Data Box Disk - See later scope it's a physical disk that send to Azure Center.