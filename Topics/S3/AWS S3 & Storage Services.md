Day 10: AWS S3 & Storage Services  

  52. S3 Bucket Versioning - Hands-on  
- Uploaded and modified `index.html`.  
- Deleted an object, which created a delete marker.  
- Deleted the delete marker, which restored the previous version of the object.  

---

  53. S3 Server Access Logging  
🔹 What it does?  
- Logs every request (authorized or denied) made to an S3 bucket into another S3 bucket.  

🔹 Why is it useful?  
✔️ Audit purposes & compliance.  
✔️ Helps in Root Cause Analysis (RCA) of issues.  
✔️ Tracks suspicious access patterns.  
✔️ Logged data can be analyzed using data analytics tools.  

---

  54. S3 Replication (CRR & SRR)  
🔹 Cross-Region Replication (CRR)  
- Replicates objects across different AWS regions.  
- Use cases: Compliance, security, disaster recovery, and latency reduction.  

🔹 Same-Region Replication (SRR)  
- Replicates objects within the same AWS region.  
- Use cases: Data sovereignty laws, log aggregation, and dev-test separation.  

🔹 Key points for replication  
✔️ Can replicate all objects or only specific ones (using prefixes/tags).  
✔️ Supports S3 Batch Replication for existing objects.  
✔️ Versioning must be enabled on both source and destination buckets.  
✔️ Replication is asynchronous.  

---

  55. S3 Replication (CRR & SRR) - Hands-on  

---

  56. S3 Storage Classes - Hands-on  

---

  57. S3 Object Lock & Glacier Vault Lock  
🔹 S3 Object Lock  
✔️ Follows WORM (Write Once, Read Many) model.  
✔️ Prevents object deletion for a specified retention period.  
✔️ Can be applied to individual objects or entire buckets.  
✔️ Automatically enables versioning.  
✔️ Ideal for business-critical data protection.  

🔹 Glacier Vault Lock  
✔️ Also follows the WORM model.  
✔️ Locks the vault policy permanently (cannot be changed).  
✔️ Helps with compliance and long-term data retention.  
✔️ Allows users to define policies on how archives should be handled.  

---

  58. Shared Responsibility Model for S3  
- AWS is responsible for: Infrastructure, durability, and availability.  
- Customer is responsible for: Data security, encryption, and access control.  

---

  59. AWS Cloud-Native Storage Options  
✅ Block Storage: EBS, EC2 Instance Store  
✅ File Storage: EFS  
✅ Object Storage: S3, Glacier  

---

  60. AWS Storage Gateway  
🔹 What it does?  
Acts as a bridge between on-premises storage and S3 in the cloud.  

🔹 Use Cases:  
✔️ Disaster Recovery  
✔️ Backup & Restore  
✔️ Storage Tiering  

🔹 Types of AWS Storage Gateway  
1️⃣ File Gateway – Stores files in S3 using NFS/SMB protocols.  
2️⃣ Volume Gateway – Block storage backed by S3 snapshots.  
3️⃣ Tape Gateway – Virtual tape library for backup purposes.  

---

  61. Amazon S3 - Summary  
✔️ Buckets vs Objects – Globally unique bucket names, objects stored in a region.  
✔️ S3 Security – IAM Policies, Bucket Policies, S3 Encryption.  
✔️ S3 Websites – Host static websites using S3.  
✔️ S3 Versioning – Maintain multiple object versions, prevent accidental deletes.  
✔️ S3 Access Logs – Log all requests made to an S3 bucket.  
✔️ S3 Replication – Supports Same-Region (SRR) and Cross-Region (CRR) replication.  
✔️ S3 Storage Classes – Standard, IA, Intelligent Tiering, Glacier, Glacier Deep Archive.  
✔️ S3 Lifecycle Rules – Automate object transitions between storage classes.  
✔️ S3 Glacier Vault Lock / Object Lock – Enforce WORM (Write Once, Read Many) policies.  
✔️ Snow Family – Physical device to transfer large data sets to AWS.  
✔️ OpsHub – Desktop app to manage Snow Family devices.  
✔️ Storage Gateway – Hybrid cloud storage solution to extend on-premises data to AWS.  



