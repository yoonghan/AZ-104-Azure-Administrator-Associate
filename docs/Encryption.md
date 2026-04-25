# Encryption

## Customer Managed Keys
1. If you use Customer-Managed Keys (CMK), the Azure Key Vault storing those keys must have both Soft Delete and Purge Protection enabled.
2. If CMK is lost, then the data cannot be decrypted.
3. Key Vault are encryption are region based. This applies to Microsoft-managed key too.
    1. In the same region as the disk. (Default)
    2. In a different region than the disk. Requires Cross-region replication to be enabled on the Key Vault.

## Creation
1. Put into Key Vault.
2. Enable Soft Delete and Purge Protection.
3. Ensure Role have access to Key Vault.
4. Create a Disk Encryption Set (DES), with Key Vault and Key. See DEK/DES work.
5. Add the DES to the Disk.
6. Associate Disk to VM.
7. Similar steps for:
    - Azure Storage Account
    - Azure SQL Database
    - Azure SQL Managed Instance

### How DES work
1. When you perform Step 5 (Add DES to the Disk):
    - Azure generates a brand new DEK (AES-256) for that specific disk.
    - Azure sends that DEK to your Key Vault.
    - Your Key Vault uses your KEK (the RSA key) to encrypt the DEK.
2. The Encrypted DEK is then stored in the disk's metadata.
3. When you perform Step 6 (Associate Disk to VM/Start VM):
    - The VM boot process realizes the disk is encrypted.
    - The Disk Encryption Set (DES) uses its Managed Identity to go to Key Vault.
    - It says: "Please use my KEK to decrypt this DEK for me."
    - Once the DEK is "unwrapped," it is loaded into the host's memory to handle the disk I/O.

### DEK (Data Encryption Key):
1. What it is: A symmetric AES-256 key.
2. Where it is: It lives right next to your data on the storage bitstream.
3. Function: It is the "workhorse" key that actually encrypts and decrypts your data blocks at high speed.

#### KEK (Key Encryption Key):
1. What it is: The RSA 2048/3072/4096 key you created in your HSM/Key Vault.
2. Where it is: It stays safely inside your Azure Key Vault.
3. Function: It "wraps" (encrypts) the DEK.

## Key Rotation
1. Key rotation is automatic.
2. Data is encrypted with the new key after a rotation is triggered.
3. The new key is automatically used for encryption of new data.

### Extra Notes for AZ-305
1. Azure encryption at rest, encrypts data at rest (in the storage account).
2. Azure Transparent Data Encryption (TDE), encrypts data at rest (in the database). Uses AES-256 encryption.
3. Server-Side Encryption (SSE): This is the default. Encryption happens at the storage level. Data is encrypted as it’s written to the disk and decrypted as it’s read. Uses AES-256 encryption.
4. Supports Client HSM (Customer Managed Keys) encryption of RSA (speed vs bit long security):
        - 2048-bit
        - 3072-bit
        - 4096-bit
5. Requires Key Vault Premium tier to support Client HSM.
