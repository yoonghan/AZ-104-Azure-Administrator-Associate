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