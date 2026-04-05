# Virtual Machines

![Link to VM Size](https://learn.microsoft.com/en-us/azure/virtual-machines/)

## Sizes
Checkout from Size->Overview in Azure Learn site. Principal is CPU vs Memory.

## Availability Set
1. Split to
    - Fault domain = Physical. This is on diff rack.
    - Update domain = Software. Use for software update/shutdown.
2. Default is 3. Has a 

## Availability Zone
1. Region always have 3 AZs
2. Az cannot be switch to Availability Set, so are AS to AZ.
3. Data transfer between AZ cost $, within AZ is free.

## VM Scale Set
1. Controlled by Load Balancer to add remove servers.
2. 2 Types of orchestration:
    - Uniform (serverless)
    - Flexible (has VM/NIC/Disk)
3. Max of 100 groups.
4. Load balancer can use for AZ or AS. Question is what is Fault Domain for?
