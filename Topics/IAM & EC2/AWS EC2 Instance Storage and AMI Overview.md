Day 5: AWS EC2 Instance Storage and AMI Overview

---

16. Amazon EBS (Elastic Block Store) Volume

- Definition:  
  A block-level storage device attached to EC2 instances, functioning like a hard drive.  

- Key Features:  
  - Durable & Flexible: Persistent storage even after instance termination.  
  - AZ Locked: Must be in the same Availability Zone as the EC2 instance.  
  - Attach/Detach: Easily detachable and re-attachable to other instances.  
  - Provisioned Capacity: Billed based on allocated GB and IOPS.  
  - Multiple Volumes: One instance can have multiple EBS volumes, but each volume can attach to only one instance.  

- Latency:  
  - Network-based storage may introduce slight latency.  

- Moving Volumes Across AZs:  
  - Requires creating a snapshot and restoring it in another AZ.

---

17. EBS - Delete on Termination Attribute

- Purpose:  
  Controls whether an EBS volume is deleted when an EC2 instance is terminated.  

- Default Behavior:  
  - Root Volume: Deleted on termination (enabled).  
  - Additional Volumes: Persist after termination (disabled).  

- Configuration:  
  - Can be modified via AWS Console or AWS CLI.  
  - Use Case: Preserve root volume data after instance termination.  

---

EBS Volume Types

1. SSD-backed Volumes (For IOPS-intensive Workloads):

- General Purpose SSD (gp3, gp2):  
  - gp3: Customizable IOPS & throughput.  
    - Baseline: 3,000 IOPS, 125 MB/s  
    - Max: 16,000 IOPS, 1,000 MB/s  
  - gp2: IOPS scales with volume size (deprecated).  

- Provisioned IOPS SSD (io1, io2):  
  - Designed for critical, low-latency workloads.  
  - io2: Higher durability (99.999%) and IOPS.  
    - Max IOPS: 256,000 (with io2 Block Express).  
  - io1: Max IOPS: 64,000.

2. HDD-backed Volumes (For Throughput-intensive Workloads):

- Throughput Optimized HDD (st1):  
  - Use Case: Big data, data warehouses, log processing.  
  - Max Throughput: 500 MB/s.  

- Cold HDD (sc1):  
  - Use Case: Archival and infrequently accessed data.  
  - Max Throughput: 250 MB/s.  
  - Lowest cost per GB.  

3. Magnetic (Standard - Deprecated):  
- Legacy storage, phased out in favor of SSD and HDD.

---

18-20. EBS Volume Lifecycle

- Creation:  
  - Via AWS Console or CLI.  

- Attachment:  
  - Must be attached to an EC2 instance in the same AZ.  

- Persistence:  
  - Controlled by the Delete on Termination setting.  

---

21-22. EBS Snapshots

- Definition:  
  Point-in-time backup of an EBS volume.  

- Use Cases:  
  - Disaster recovery  
  - Data migration  
  - Backup compliance  

- Features:  
  - Snapshots can be copied across AZs and regions.  
  - Used to restore volumes.  

- Hands-on:  
  - Created a snapshot of a volume → Restored a new volume from the snapshot.  

---

23. Amazon Machine Image (AMI)

- Definition:  
  A template that contains the information required to launch EC2 instances.  

- AMI Components:  
  - Operating System (OS)  
  - Preinstalled software  
  - Launch permissions  
  - Root volume template  
  - Storage mappings  

- AMI Types:  
  - Public AMI: Provided by AWS.  
  - Custom AMI: Created and managed by the user.  
  - AWS Marketplace AMI: Third-party AMIs (free/paid).  

- Customization:  
  - Install OS/software → Create AMI → Faster deployment.  

- Region-Specific:  
  - AMIs are region-bound but can be copied to other regions.  

---

24-26. AMI Lifecycle

- Process:  
  1. Launch and configure an EC2 instance.  
  2. Stop the instance.  
  3. Create an AMI (includes EBS snapshots).  
  4. Launch new instances from the AMI.  

- Hands-on:  
  - Created an EC2 instance → Customized it → Created an AMI → Launched a new EC2 instance using that AMI.  

---

27. EC2 Image Builder

- Purpose:  
  Automates the creation, maintenance, and validation of EC2 AMIs and container images.  

- Features:  
  - Automates AMI updates and deployments.  
  - Can be scheduled (e.g., weekly updates).  
  - Free service (charged only for used resources).  

---  

This summary covers EC2 storage (EBS), snapshots, AMI creation, and automation using EC2 Image Builder.