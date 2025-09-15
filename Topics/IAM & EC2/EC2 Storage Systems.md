Day 6 Highlights: EC2 Storage Systems

28. EC2 Instance Store
- Definition: Temporary block-level storage directly attached to the host server for an EC2 instance.
- Key Features:
  - High performance and low latency.
  - Suitable for buffer, cache, temporary files, and scratch data.
  - Data is lost on instance stop/termination or crashes.
  - Not automatically backed up—manual backups and replication are required.
- Limitations:
  - Only available on certain EC2 instance types.
  - Unsuitable for critical or persistent data.

---

29. Amazon Elastic File System (EFS)
- Definition: Fully managed, scalable, and elastic network file system that can be shared by multiple EC2 instances and other AWS services.
- Key Features:
  - Elastic & Managed: Automatically scales, no manual intervention required.
  - Cost-Effective: Pay only for used storage; tiering available for infrequently accessed data.
  - Concurrent Access: Shared access for multiple instances.
  - High Availability: Data redundancy across AZs.
- Performance Modes:
  - General Purpose: Low latency for regular use cases.
  - Max I/O: For highly parallel workloads.
- Storage Classes:
  - Standard: For frequently accessed files.
  - Infrequent Access (IA): Cost-optimized for rarely accessed files.

---

30. EFS Infrequent Access (EFS-IA)
- Purpose: Cost-optimized storage class for files not accessed daily.
- Cost Efficiency: Up to 92% lower cost compared to standard EFS storage.
- Automation: Files are automatically moved to EFS-IA based on lifecycle policies.

---

31. Shared Responsibility Model for EC2 Storage
- AWS Responsibility: Infrastructure, hardware, and availability of storage systems.
- User Responsibility: Configuring storage, backups, and data security.

---

32. Amazon FSx for Windows File Server
- Managed file storage for Windows applications, supporting SMB protocol and Active Directory integration.

---

33. Amazon FSx for Lustre
- High-performance file system for Linux-based workloads, designed for machine learning, HPC, and big data analytics.

---

34. EC2 Storage Summary
- EBS: Durable network drives attached to EC2 instances. Supports snapshots for backup and migration across AZs.
- AMI: Pre-configured images for fast instance launches with customizations.
- EC2 Instance Store: High-performance local storage with data persistence tied to instance lifecycle.
- EFS: Elastic, shared storage system for multiple instances.
- EFS-IA: Cost-optimized tier for infrequent access.
- FSx for Windows: Network file storage for Windows servers.
- FSx for Lustre: High-performance file system for Linux workloads.

---

