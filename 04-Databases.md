# Databases

## Relational Database

Relational database are what most of us are all used to. They have been around since the 70's. Think of a traditional spreadsheet, with the database

### Relational Database on AWS

- SQL Server
- Oracle
- MySQL Server
- PostgreSQL
- Aurora
- MariaDB

### Features on AWS

- Multi-AZ for Disaster Recovery
- Read Replicas for Performance

## Non Relational Databases


## Data Warehousing

Used for business intelligence. Tools like Cognos, Jaspersoft, SQL Server Reporting Services, Oracle Hyperion, SAP NetWeaver.
Used to pull in very large and complex data sets. Usually used by management to do queries on data (such as current performance vs targets, etc)

## OLTP vs OLAP

Online Transaction Processing (OLTP) differs from Online Analytics Processing (OLAP) in terms of the types of queries you will run. Usually an OLTP is for fast query, getting a row of information, OLAP is use for getting a large number the records, to do calculations at the data.
Data Warehousing databases use different type of architecture both from a database perspective and infrastructure layer (at AWS this is Redshift).

## ElastiCache

Elasticache is a web service that makes it aesy to deploy, operate and scale an in-memory cache in the cloud. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.
Elesticache supports two open-source in-memory caching engines:
- Meemcached
- Redis

## RDS

- RDS runs on virtual machines
- You canot log in those operating systeams however
- Patching of the RDS Operating System and DB is Amazon's responsibility
- RDS is NOT serverless
- Aurora Serveless IS Serverless

### Backups

There are two different types of BAckups for RDS:
- Automated Backups
- Database Snapshots

#### Automated Backups

Allow you to recover your database to any point in time within a "retention period". The retention period can be between one and 35 days. Automated Backups will take a full daily snapshot and will also store transaction logs throughout the day. When you do a recovery, AWS will first choose the most recent daily back up and then apply transaction logs throughout the day. This allows you to do a point in time recovery down to a second, within the retention period.
Automated Backups are enabled by default. The backup data in stored in S3 and you get free storage space equal to the size of your database. So if you have an RDS instance of 10 Gbs, you will get 10Gb worth of storage.
Backups are taken within a defined window. During the backup window, storage I/O may be suspended while your data is being backed up and you may experience elevated latency.

#### Database Snapshots

DB Snapsshots are done manually (ie they are user initiated). They are stored even after you delete the original RDS instance, unlike automated backups.

#### Restoring Backups

Whenever you restore either an Automatic Backup or a manual Snapshot, the restored version of the database will be a new RDS instance with a new DNS endpoint.

### Encryption at Rest

Encryption at Rest is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB e Aurora. Encryption is done using the AWS Key Management Service (KMS). Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automatic backups, read replicas and snapshots.

### Multi-AZ

Multi-AZ allows you to have an exact copy of your production database in another Availability Zone. AWS handles the replication for you, so when your production database is written to, this write will automatically be synchronized to the stand by database.
In the event of planned database maintennance, DB Instance failure, or an Avalability Zone failure, Amazon RDS will automatically failover to the standby so that database operations can resume quickly without administrative intervention.

**THIS IS FOR DISASTER RECOVERY ONLY** it is nho primarily used for improving performance. For performance improvement, you nedd Read Replicas.

#### Available for

- SQL Server
- Oracle
- MySQL SErver
- PostgreSQL
- MariaDB

**TRICK, NOT Aurora** - Aurora have Multi-AZ on by nature.

### Read Replicas

Read Replicas allow you to have a read-only copy of your production database. This is achieved by using Asynchronous replication from the primary RDS instance to the read replica. You use read replicas primarily for very read-heavy database workloads.

#### Available for

- Oracle
- MySQL SErver
- PostgreSQL
- MariaDB
- Aurora

#### Things to Know about Read Replicas

- Used for scaling, not for DR!
- Must have automatic backups turned on in order to deploy a read replica.
- You can have up to 5 read replica copies of any database.
- You can have read replicas of read replicas (but watch out for latency)
- Each read replica will have its own DNS end point
- You can have read replicas that have Multi-AZ
- You can create read replicas of Multi-AZ source databases
- Read replicas can be promoted to be their own databases. This breaks the replication.
- You can have a read replica in a second region

## DynamoDB

Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed database and supports both document and key-value data models. Its flexible data model and realiable performance make it a great fit for mobile, web, gaming, ad-tech, IoT and many other applications.

### Basics of DynamoDB

- Stored on SSD storage
- Spread across 3 geographically distinct data centres
- Two Different Types of Reads Mods:
  - Eventual Consistent Reads (Default)
  - Strong Consistent Reads
  
#### Eventual Consistent Reads

Consistency across all copies of data is usually reached within a second. Repeating a read after a short time should return the update date (best read performance).

#### Strong Consistent Reads

A strongly consistent read returns a result that reflects all writes that received a successful response prior to the read.

## Redshitf

Amazon Redshitf is fast and powerfull, fully managed, petabyte-scale data warehouse service in the cloud. Customers can start small for just $0.25 per hour with no commitments or upfront cost and scale to a petabyte or more for $1,000 per terabyte per year, less than tenth of most other data warehousing solutions.

### Redshift Configuration

- Single Node (160GB)
- Multi-Node
  - Leader Node: manages client connections and receives queries
  - Compute Node: store data and perform queries and computations. Up to 128 Compute Nodes.
  
### Advanced Compression

Columnar data stores can be compressed much more than row-based data stores because similar data is sored sequentially on disk. Amazon Redshift employs multiple compression techniques and can often achieve significant compression relative to traditional relational data stores. In addition, Amazon Redshift doesnot require indexes or materialized views and so uses less space than traditional relational database systems. When loading data intro an empty table, amazon Redshift automatically samples your data and delects the most appropriate compression scheme.

### Massively Parallel Processing (MPP)

Amazon Redshift automatically distributes data and query load across all nodes. Amazon Redshift makes it easy to add nodes to your data warehouse and enables you to maintain fast query performance as your data warehouse grows.

### Backups

- Enabled by default with a 1 day retention period
- Maximum retention period is 35 days
- Redshift always attempts to maintain at least three copies of your date (the original and replica on the compute nodes and a backup in Amazon S3)
- Redshift can also asynchronously replicate your snapsshots to S3 in another region for disaster recovery

### Pricing

Compute Node Hours (total number of hours you run across all your compute nodes for the billing period. You are billed for 1 unit per node hour, so a 3 node data warehouse cluster running persistently for an entire month would incur 2,160 instance hours. You will not be charged for leader node hours, only compute nodes will incur charges)
Also there will be charged for Backups and Data Transfer (only within a VPC, not outside it)

### Security Considerations

- Encrypted in transit using SSL
- Encrypted at rest using AES-256 encryption
- By default ReadShift takes care of key management
- You can manage your own keys through HSM or AWS KSM

## Availability

- Currently only available in 1 AZ
- Can restore snapsshots to new AZs in the event os an outage

## Aurora

Amazon Aurora is a MySQL and PostgreSQL-compatible relational database engine that combines the speed and availability of high-end commercial databases with the simplicity and cost-effectiveness of open source databases. Amazon aurora provides up to five times better performance that MySQL and three times better than PostgreSQL databases at a much lower price point, whilst delivering similar performance and availability.

### Things to Know about Aurora

- Start with 10 GB, Savles in 10GB increments to 64TB (storage autoscaling)
- Compute resources can scale up to 22vCPUs and 244GB of Memory
- 2 copies of your data is contained in each availability zone, with minimum of 3 availability zones (6 copies of your data).

### Scaling Aurora

Designed to transparently handle the loss of up two copies of data without affecting database write availability and up to three copies without affecting read availability.
Aurora storage is also self-healing. Datablocks and disks are continuously scanned for errors and repaired automatically.

### Aurora Replicas

- Aurora Replicas (currenctly 15)
- MySQL Read Reaplicas (currently 5)

### Backups

- Automated backups are always enabled on Amazon AuroraDB instances. Backups do not impact database performance.
- You can also take snapshots with Aurora. This also does not impact on performance.
- You can share Aurora Snapshots with other AWS Accounts.

## ElastiCache

ElastiChache is a web service that makes it easy to deploy, operate and scale an in-memory cache in the cloud. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.

### Memchached vs Redis

| Requirement | Memchached | Redis |
|-------------|------------|-------|
| Simple Cache to Offload DB | Yes | Yes |
| Ability to scale horizonlally | Yes | Yes |
| Multi-threaded performance | Yes | No |
| Advanced data types | No | Yes |
| Ranking/Sorting data sets | No | Yes |
| Pub/Sub Capabilities | No | Yes |
| Persistence | No | Yes |
| Multi-AZ | No | Yes |
| Bachup & Restore Capabilities | No | Yes |

# Summary

- RDS = OLTP
- RDS can be SQL server, MySQL, PostgreSQL, Oracle, Aurora, MariaDB
- DynamoDB - NoSQL
- RedShift = OLAP
- Elasticached, Memchached (Multi-threaded performance) and Redis (Ad type, Rank/Sort, Pub/Sub, Multi-AZ, Restore)
- **RDS** runs on virtual machines, no ssh allowed, patching of RDS OS and DB is Amazon's responsibility
- RDS NOT Serveless, only AURORA IS Serverless
- RDS have two type of Backups, Automated and Snapshots
- RDS Read Reaplicas:
  - Multi-AZ
  - Increase PERFORMANCE
  - Must have backups turned on
  - Can be in different regions
  - Can be MySQL, PostgreSQL, MariaDB, Oracle, Aurora
  - Can be promoted to master, this will break the Read Reaplica
- RDS Multi-AZ is used for DISASTER RECOVER and you can force a failover from one AZ to another by rebooting the RDS instance
- Encrytion at reas is supported for MySQL, Oracle, SQL Server, PostgreSQL, MariaDB & Aurora. Encryption is done using the AWS KMS. Once your instance is encrypted, the data stores at rest in the underlying storage is encrypted, as are its automated backups, read replicas and snapshots.
- **DynamoDB** stored on SSD storage, Spread Across 3 geographically distinct data centres
- DaynamoDB can have:
  - Eventual Consistent Reads (Default)
  - Strongly Consistent Reads
- **Redshift** (AWS BI), only at one AZ, backups (1 day by default, max of 35 days) always try to maintain at least three copies of your data (the original and a replica in the compute nodes and a extra in S3).
- Readshift can also asynchronously replicate your snapsshots to S3 in another region for disaster recovery.
- **Aurora** 2 copies of your data is contained in each availability zone, with minimum of 3 availability zones. Total 6 copies of your data.
- Yoy can share Aurora Snapshots with other AWS accounts.
- 2 types of reclicas available. Aurora Replicas and MySQL replicas. Automated failover is only available with Aurora Replicas.
- Aurora has automated backups turned on by default. You can also take snapshots with Aurora. You can share these snapshots with other AWS accounts.
- **Elasticache** use to increase databases and web application performance
  - Redis is Multi-AZ, can backups and restored
  - Memcached use if you need scale horizontally
