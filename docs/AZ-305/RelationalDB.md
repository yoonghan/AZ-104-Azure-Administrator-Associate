# Relational DB

## SQL Server
1. Service Tier:

  - General Purpose (GP): CPU, Memory, IOPS are balanced. Good for most workloads.
  - Business Critical (BC): High IOPS, low latency. Good for OLTP.
  - Hyperscale (HS): Large DB size, high availability. Good for Big Data.
2. PAAS SKU:

  - Basic
  - Standard
  - Premium
3. Features:

  - SQL Server Masking: Dynamic data masking keeps sensitive data secure by masking it to non-privileged users. For example, you can mask credit card numbers so that only users with specific database roles can see the full number. 
  - Threat Detection: Monitors the database for suspicious activities and alerts you to potential threats. It can detect anomalies such as unusual login attempts, SQL injection attacks, and data exfiltration attempts. 
  - Encryption:
    - Deterministic encryption: Always generates the same encrypted value for the same plaintext value. Use this when you need to search or group by the encrypted column.
    - Randomized encryption: Generates a different encrypted value for the same plaintext value. Use this when you need to protect data from hackers, and you don't need to search or group by the encrypted column.

## Types of SQL Server
1. Azure SQL Database: Paas but not 100% compatible with SQL Server. It has limited features of SQL Server.
2. SQL Server Managed Instance : Paas but 100% compatible with SQL Server. It has almost all features of SQL Server. Requires a VNet.


3. SQL Server on Azure VM: IaaS. Full control over the SQL Server.
4. Azure SQL Edge: SQL Server designed for IoT and edge devices.

| Feature | SQL Managed Instance | Azure SQL Database | SQL Server on Azure VM |
| --- | --- | --- | --- |
| Instance-level features | Yes | No | Yes |
| Database-level features | Yes | Yes | Yes |
| VNet required | Yes | No | Yes |
| Multi DB Connection | Yes | No | Yes |
| Service Broker Support | Yes | No | Yes |
| Cross DB Query | Yes | No | Yes |
| Cross DB Transaction | Yes | No | Yes |
| Linked Servers | Yes | No | Yes |
| SQL Agent | Yes | No | Yes |
| Cross-VNet access | Yes | No | Yes |


4. High Availabilty and Disaster Recovery (HADR):

| HA/DR method | SQL Managed Instance | Azure SQL Database | SQL Server on Azure VM |
| --- | --- | --- | --- |
| Geo- Replication | Yes | Yes | Yes |


### Azure SQL Database
![Azure SQL Database](azuresql.png)

1. vCore: A vCore is a virtual core. You choose the number of virtual cores and have greater control over your compute costs. This option supports the Azure Hybrid Benefit for SQL Server and reserved capacity (pay in advance).
2. DTU: A DTU (Database Transaction Unit) is a combined measure of compute, storage, and I/O resources. The DTU option is an easy, preconfigured purchase option.
3. Serverless: Split to:
    - General Purpose, automatically scales compute and charges for what you use.
    - Hyperscale, supports large storage, up to 100TB.
4. Elastic Database Pool: Buy a set of compute and storage resources to share among all SQL databases in an elastic pool.
5. Private link support.

### Azure Managed Instance Database
1. Either 
    - Single Instance
    - Instance Pool