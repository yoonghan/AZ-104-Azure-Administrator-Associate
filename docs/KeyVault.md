## Key Vault

## Tiers:
1. Standard: 
    - soft delete, purge protection, private endpoint
    - non-HSM, 2000 transactions/5 min
2. Premium (keyword FIPS 140 or fully managed): 
    - 20,000 transactions/5 min
    - Azure Key Vault Premium supports HSM-protected symmetric keys through the oct-HSM key type. Symmetric keys in vaults are HSM-backed only and require a Premium vault.

## Features
- Rotation: Auto-rotation every 1 year
- Auditing
- Centralized Key Management
- Networking: Private Endpoint, Service Endpoint, or IP Firewall and virtual network rules
- Purge and delete protection
- Stores key, certificate or HSM (custom encryption)
