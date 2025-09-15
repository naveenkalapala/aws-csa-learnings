Day 3: AWS Learning Notes

---

7. Creating an EC2 Instance with User Data (Bootstrap Script):

- User Data Script: Allows automation by running commands at the first launch of an EC2 instance.  
- Purpose: Automates tasks like installing software, updating packages, and configuring applications.  
- Execution: Runs only once during the initial boot.  
- Example:  
  
  !/bin/
  sudo yum update -y
  sudo amazon-linux-extras install docker
  sudo service docker start
  sudo usermod -a -G docker ec2-user
  

---

8. Establishing SSH Connection to EC2 Instance and Checking Docker Installation:

- SSH Connection:  
  
  ssh -i "key_pair.pem" ec2-user@<EC2-Public-IP>
  

- Verify Docker Installation:  
  
  docker --version
  sudo service docker status
  

---

9. EC2 Instance Types - Overview:

General Purpose (T & M Family):  
- Balanced compute, memory, and networking.  
- Example: `m5.8xlarge` → 32 vCPUs, 128 GiB RAM.  
- Use Cases: Web servers, development environments, microservices.  

Compute Optimized (C Family):  
- High-performance processors for compute-intensive tasks.  
- Use Cases: Batch processing, gaming servers, machine learning inference.  

Memory Optimized (R Family):  
- High-speed memory access for large datasets.  
- Use Cases: In-memory databases, real-time big data analytics.  

Accelerated Computing:  
- Hardware accelerators (GPUs, FPGAs) for specialized workloads.  
- Use Cases: Generative AI, HPC, graphics rendering.  

Storage Optimized:  
- High IOPS and throughput for data-intensive applications.  
- Use Cases: NoSQL/relational databases, real-time analytics.  

HPC Optimized:  
- Optimized for high-performance computing workloads.  
- Use Cases: Simulations, scientific modeling, deep learning.  

---

10. Security Groups:

- Definition: Virtual firewalls that control inbound and outbound traffic for EC2 instances.  
- Rules:  
  - Allow rules only (no deny rules).  
  - Can allow traffic by IP address or another security group.  
  - Authorise I.P ranges - IPv4 & IPv6
- Default Behavior:  
  - Inbound: All traffic is blocked by default.  
  - Outbound: All traffic is allowed by default.  
- Best Practice:  
  - Use a separate security group for SSH access.  

- Common Security Group Ports:  
  - 22: SSH (Linux login)  
  - 21: FTP (File upload)  
  - 22: SFTP (Secure file upload)  
  - 80: HTTP (Unsecured websites)  
  - 443: HTTPS (Secured websites)  
  - 3389: RDP (Windows login)  

- Troubleshooting:  
  - Timeout errors: Usually due to security group misconfiguration.  
  - Connection refused: Typically an application issue.  

---

These topics provide a solid understanding of launching EC2 instances, managing connections, and configuring security in AWS.