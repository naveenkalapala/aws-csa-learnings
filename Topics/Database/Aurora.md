What is Amazon Aurora?

Amazon Aurora is a **fully managed, high-performance relational database engine** built for the cloud by AWS.

- Aurora is a **proprietary technology** from AWS (not open-sourced)  
- Compatible with **PostgreSQL** and **MySQL**  
- **Cloud optimized**:  
  - Up to **5x performance** over MySQL on RDS  
  - Over **3x the performance** of PostgreSQL on RDS  
  - Designed for modern, high-throughput cloud apps  
- **Storage auto-scales** in 10 GB increments, up to **64 TB**  
- Costs about **20% more than RDS**, but offers better efficiency  
- **Not included in the Free Tier**  

#Compatibility

Aurora supports:
- MySQL  
- PostgreSQL  
- MariaDB  
- Oracle  

---

Aurora Architecture (High-Level)

```text
                     +---------------------------+
                     |     Application Layer     |
                     |  (EC2, Lambda, etc.)      |
                     +------------+--------------+
                                  |
                                  v
                       +---------------------+
                       |   Aurora Cluster     |
                       +----------+----------+
                                  |
               +------------------+-------------------+
               |                                      |
     +---------v---------+                  +---------v---------+
     |  Primary Instance |  ← Read/Write    |  Aurora Replicas  |
     |  (Writer Node)    |                  |  (Up to 15 Readers)|
     +-------------------+                  +-------------------+
                                  |
                                  v
                        +----------------------+
                        | Aurora Storage Layer |
                        | (6 copies across 3 AZs)|
                        +----------------------+
````

---

Aurora Deployment Options

| Option                   | Description                                                      |
| ------------------------ | ---------------------------------------------------------------- |
| **Aurora Provisioned**   | Fixed DB instance sizes; managed scaling                         |
| **Aurora Serverless v2** | Auto-scales DB compute capacity in seconds                       |
| **Global Database**      | Multi-region DB with <1s replication lag for DR and read scaling |
| **Read Replicas**        | Scale read workloads with up to 15 replicas                      |
| **Aurora Multi AZ**      | Deploy in 2 AZs for high availability                            |
| **Aurora Serverless v1** | Auto-scales DB compute capacity in minutes                       |

---

Read Replicas

* Up to **15 Aurora Replica Instances**
* Can be **promoted** to standalone DB instances
* Used for **read scaling** and **disaster recovery**
* Supports **cross-region read scaling**
* **Data is only written to the primary instance**
* **Typical replica lag < 1 second**

---

Multi-AZ Deployments

* Deployed in **2 Availability Zones** for high availability
* Data is **automatically synced** to the standby replica
* **Instant failover** supported
* **Writes/reads go only to the primary instance**
* Only **one AZ can act as failover**

---

Multi-Region Deployments

* Deployed in **multiple regions** for disaster recovery
* Incurs **replication costs** between regions
* Offers **low-latency access** from local region
* Great for **global performance and resilience**

---

When to Use Amazon Aurora

| Use Case                           | Aurora is Ideal If You Need...   |
| ---------------------------------- | -------------------------------- |
| **High performance**               | Low latency, high throughput     |
| **Scalability**                    | Auto-scaling reads/writes        |
| **High availability**              | Built-in failover and redundancy |
| **MySQL/PostgreSQL compatibility** | Migrate with minimal changes     |
| **Cost-effective alternative**     | Cheaper than Oracle/SQL Server   |

```

