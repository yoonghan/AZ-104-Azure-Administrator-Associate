# Encryption

## Customer Managed Keys
1. If you use Customer-Managed Keys (CMK), the Azure Key Vault storing those keys must have both Soft Delete and Purge Protection enabled.

## Creation
1. Put into Key Vault.
2. Enable Soft Delete and Purge Protection.
3. Ensure Role have access to Key Vault.
4. Create a Disk Encryption Set (DES), with Key Vault and Key.
5. Add the DES to the Disk.
6. Associate Disk to VM.
7. Similar steps for:
    - Azure Storage Account

## Key Rotation
1. Key rotation is automatic.
2. Data is encrypted with the new key after a rotation is triggered.
3. The new key is automatically used for encryption of new data.