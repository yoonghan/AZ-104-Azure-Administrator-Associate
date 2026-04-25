# Virtual Machines
[Link to VM Size](https://learn.microsoft.com/en-us/azure/virtual-machines/)

| Feature | Description |
| --- | --- |
| **VM Size** | Determines CPU, RAM, and storage performance. |
| **OS Disk** | The boot disk for the VM. Can be Premium SSD, Standard SSD, Standard SSD LRS (not available for OS disk), Ultra Disk, Ultra Disk LRS (not available for OS disk), Standard HDD. |
| **Data Disks** | Additional disks attached to the VM for data storage. |
| **Network Interface (NIC)** | Connects the VM to the virtual network. |
| **Public IP Address** | Optional address for internet access. |
| **Availability Set** | Spreads VMs across physical hardware to prevent downtime. |
| **Availability Zone** | Spreads VMs across different data centers for zone-level redundancy. |
| **VM Scale Set** | Automatically manages and scales a group of identical VMs. |
| **Azure Backup** | Service for backing up and restoring VMs. |
| **Azure Site Recovery** | Service for disaster recovery and business continuity. |
| **Azure Monitor** | Service for monitoring VM performance and health. |
| **Azure Advisor** | Provides recommendations for optimizing VM performance and cost. |
| **Azure Policy** | Enforces organizational standards and assesses compliance. |
| **Azure Role-Based Access Control (RBAC)** | Controls access to VM resources. |
| **Azure Disk Encryption** | Encrypts VM disks for security. |
| **Azure Security Center** | Provides security management and threat protection. |
| **Azure Advisor** | Provides recommendations for optimizing VM performance and cost. |
| **Azure Policy** | Enforces organizational standards and assesses compliance. |
| **Azure Role-Based Access Control (RBAC)** | Controls access to VM resources. |
| **Azure Disk Encryption** | Encrypts VM disks for security. |
| **Azure Security Center** | Provides security management and threat protection. |

## Sizes
Checkout from Size->Overview in Azure Learn site. Principal is CPU vs Memory. This is vertical scaling.

## Availability Set
1. Split to
    - Fault domain = Physical, same network and hardware. This is on diff rack.
    - Update domain = Software. Use for software update/shutdown.
2. Control on domain/fault

| Setting | Min (Allowed) | Max (Allowed) | Common Default |
| --- | --- | --- | --- |
| Fault Domains | 1 | 3 (depends on region) | 2 |
| Update Domains | 1 | 20 | 5 |

3. Splitting is based on Round Robin, If you have an Availability Set configured with 3 Fault Domains (FD) and 5 Update Domains (UD), the placement looks like this as you add VMs:
4. Update Domain group, restarts together.
5. Restarting VM individually, does not follow the UD group and may reorder the Update Domain. Also Placement is Immutable.
6. If there is > X update domain, then there must be >= X fault domain. It does not have to be exact. But if UD is 1, FD must be 1, if UD is 2, FD must be 1 or 2 ...

| VM Number | Fault Domain (Rack) | Update Domain (Reboot Group) |
| --- | --- | --- |
| VM 1 | FD 0 | UD 0 |
| VM 2 | FD 1 | UD 1 |
| VM 3 | FD 2 | UD 2 |
| VM 4 | FD 0 (Recycles) | UD 3 |
| VM 5 | FD 1 | UD 4 |
| VM 6 | FD 2 | UD 0 (Recycles) |

## Availability Zone
1. Region always have 3 AZs
2. Az cannot be switch to Availability Set, so are AS to AZ.
3. Data transfer between AZ cost $, within AZ is free.

## VM Scale Set
1. Controlled by Load Balancer to add remove servers.
2. 2 Types of orchestration that cannot be mixed:
    - Uniform (serverless) - max 100 VMs in a single Zone.
    - Flexible (has VM/NIC/Disk) - max 1000 VMs spread across AZs. Not all zone are supported.
3. Max of 100 groups.
4. Note: No longer has different SKU of basic/standard LB.
5. This is layer 4 load balancer, handling TCP/UDP. For Layer 7, requires to use Application Gateway.
6. Can only be in a Availability Zone or Availability Set, not both.
7. Only in 1 region. No cross region. Use Traffic Manager for cross-region.

### Scale in policy
[Scale-in policy](https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-scale-in-policy)
Configures to remove based on:
1. Default
    - Balance virtual machines across availability zones (if the scale set is deployed in zone-spanning configuration)
    - Balance virtual machines across fault domains (best effort)
    - Delete virtual machine with the highest instance ID
2. NewestVM - delete the newest, or most recently created virtual machine in the scale set, after balancing VMs across availability zones
3. OldestVM - delete the oldest, or least recently created virtual machine in the scale set, after balancing VMs across availability zones.

![Scaling condition](img/vmss_scaling.png)

## VM extensions
1. Used to configure and install more software on your virtual machine after the initial deployment. 
2. OS based:
    - Linux uses waagent (Linux Agent)
    - Windows uses Windows Azure VM Agent, installed by default. Has option to install diagnostic agent.
3. Can be listed with command (az vm extension list --resource-group <resource-group-name> --vm-name <vm-name>)
4. Custom script, allows shell script `https://learn.microsoft.com/en-us/azure/virtual-machines/extensions/custom-script-windows`. Don't use the Custom Script Extension to run Update-AzVM with the same VM as its parameter. The extension will wait for itself.

## Azure automation / runbook
Just a script to autoshutdown, or run some automation.

## Auto - shutdown
Optional to use runbook/automation to run this as well.

## Azure Site Recovery
Azure Site Recovery replicates workloads from a primary site to a secondary location. If an outage happens at your primary site, you can fail over to a secondary location. This failover enables users to continue to access your applications without interruption. You can then fail back to the primary location after it's up and running again. Azure Site Recovery is about replication of virtual or physical machines; it keeps your workloads available in an outage.

## Backup
1. Backup is done by Azure Backup service, a subset of Recovery Services.
2. Azure Backup doesn't limit the amount of inbound or outbound data you transfer. Azure Backup also doesn't charge for the data that is transferred.
3. VM has extension for 2 type of backup:
    - Storage: Snapshots when using an Azure VM or Azure Files.
    - Stream backup: For databases like SQL or High-performance Analytic Appliance (HANA) running in VMs.

![Virtual Machine Backup](img/vm_backup.png)

## Differences

Scope| Tool |What happens if...
--- | --- | ---
Rack Level | Fault Domains (inside Availability Set) | A single power supply or network switch on a rack fails.
Server Level | Update Domains (inside Availability Set) | Microsoft patches the physical host server where your VM lives.
Datacenter Level | Availability Zones | An entire building loses power or has a cooling failure.
Traffic Level | Load Balancer Health Probes | "A VM is ""up"" but your application (IIS/Apache/Service) has crashed."

## LifeCycle
1. Deallocated means the VM gets removed from the host, so you will not be charged for compute, but you will still be charged for storage.
2. Public IP are released for stop and deallocate.

```mermaid
flowchart TD
    Creating --> Starting --> Start --> Running --> Stopping --> Stopped
    Running --> Deallocating --> Deallocated
```

## Extra notes
1. VM must be shutdown:
    - if NIC is to be added/removed.
    - if a VM is moved from one Availability Set to another.
    - if a VM is resized to a different VM size.
2. VM doesn't need to shutdown:
    - if Public IP is to be added/removed/changed. It only takes effect when the VM is restarted.
    - if Disk is to be added/removed/resized.
    - if VM extension is to be added/removed/updated.
    - if VM is to be moved from one Availability Zone to another.
3. Disk Types:
    - OS type
    - Data type
    - Temp type
4. Only Standard HDD, Standard SSD, Premium SSD can be attached as OS disk. For data disk, all disk types are supported.
