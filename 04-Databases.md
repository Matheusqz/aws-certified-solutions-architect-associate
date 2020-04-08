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

**TRICK, NOT Aurora** Aurora have Multi-AZ on by nature.

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

## Redshitf

## Aurora

## Elasticache

### Memchached

### Redis

# Summary
