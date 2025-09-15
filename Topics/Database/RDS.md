
What is Amazon RDS?

**RDS** stands for **Relational Database Service**.  
It is a **fully managed database service** by AWS that uses **SQL as a query language**.

RDS allows you to create and manage relational databases in the cloud, eliminating the need for manual infrastructure management like OS patching, backups, and replication.

#Supported Database Engines:
- PostgreSQL  
- MySQL  
- MariaDB  
- Oracle  
- Microsoft SQL Server  
- Aurora (AWS proprietary high-performance DB)

---

Benefits of Using RDS vs Deploying on EC2

Amazon RDS is an **AWS-managed service**, while deploying a DB on EC2 requires manual maintenance.

| Feature                        | RDS (Managed)                         | EC2 (Self-Managed)               |
|-------------------------------|---------------------------------------|----------------------------------|
| Provisioning & OS Patching    | ✅ Automated                          | ❌ Manual                        |
| Backups & PITR                | ✅ Continuous backups, point-in-time  | ❌ Manual snapshot scripting     |
| Monitoring                    | ✅ Built-in dashboards (CloudWatch)   | ❌ Manual setup required         |
| High Availability             | ✅ Multi-AZ failover supported        | ❌ Must configure yourself       |
| Read Scalability              | ✅ Read replicas supported            | ❌ Custom solution needed        |
| Scaling                       | ✅ Horizontal & vertical supported    | ❌ Manual effort                 |
| Maintenance & Upgrades        | ✅ Maintenance windows supported      | ❌ Manual patching               |
| Storage                       | ✅ EBS-backed (gp2, gp3, io1, io2)     | ❌ Must configure EBS manually   |
| SSH Access                    | ❌ Not allowed                        | ✅ Full SSH access               |

> ⚠️ **Note:** RDS does **not allow SSH access** to DB instances.

---

RDS Solution Architecture (High-Level)

```text
                          +-------------------------+
                          |     User Requests       |
                          +------------+------------+
                                       |
                                       v
                       +-------------------------------+
                       |   Elastic Load Balancer (ELB)  |
                       +-------------------------------+
                                       |
                                       v
              +--------------------+       +--------------------+
              |   EC2 Instance 1   |       |   EC2 Instance 2   |  ← Auto Scaling Group (ASG)
              +--------------------+       +--------------------+
                       |                            |
                       |        Application Layer   |
                       |            (e.g., API, UI) |
                       |                            |
                       +------------+---------------+
                                    |
                                    v
                    +-------------------------------+
                    |        Amazon RDS (Primary)   |  ← Read/Write DB
                    |       (Multi-AZ enabled)      |
                    +-------------------------------+
                                    |
               +--------------------+--------------------+
               |                                         |
       +--------v--------+                    +----------v----------+
       |  RDS Standby DB |                    |     Read Replica     |
       |  (Automatic HA) |                    |  (Read-only scaling) |
       +-----------------+                    +----------------------+

                     +-------------------------------+
                     |     Amazon CloudWatch         |
                     | (Monitoring, Alarms, Metrics) |
                     +-------------------------------+

                     +-------------------------------+
                     |         IAM + Security        |
                     | (Access control & DB secrets) |
                     +-------------------------------+
````

---

✅ Summary

Amazon RDS provides a **robust, scalable, and managed** solution for relational databases on AWS.
It helps reduce operational overhead and provides enterprise features like high availability, backups, scaling, and monitoring — **without the need to manage the infrastructure yourself**.
