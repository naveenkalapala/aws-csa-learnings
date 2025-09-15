Day 2: AWS Learning Notes

---

5. Identity and Access Management (IAM):

IAM is a service that helps securely control access to AWS resources.

- IAM Users:  
  Individual user accounts with specific permissions.  

- IAM Groups:  
  Collections of users with shared permissions.  

- IAM Policies:  
  JSON documents defining permissions for users, groups, and roles.  

- IAM MFA (Multi-Factor Authentication):  
  Adds an extra layer of security by requiring a second authentication method (e.g., OTP).  

- Generating Access & Secret Keys:  
  Credentials used for programmatic access to AWS services.  

- Cloud Shell:  
  A browser-based shell for managing AWS resources without configuring a local environment.  

- IAM Roles for AWS Services:  
  Temporary permissions assigned to AWS services to interact with other AWS resources securely.  

- IAM Security Tools:  
  - IAM Credential Report: Generates a report about the status of IAM users and credentials.  
  - IAM Access Advisor: Provides details on the services that IAM users and roles have accessed.  

- Shared Responsibility Model for IAM:  
  - AWS Responsibility: Securing the infrastructure (hardware, software, networking).  
  - Customer Responsibility: Managing access controls, IAM configurations, and data protection.  

---

6. Elastic Compute Cloud (EC2):

Amazon Elastic Compute Cloud (EC2) is a web service that allows users to create and run virtual machines (instances) in the cloud

- AWS Budget Setup:  
  Allows setting custom budget limits to monitor AWS spending.

- EC2 Basics:  
  - EC2 (Elastic Compute Cloud): Infrastructure as a Service (IaaS) for renting virtual machines.  
  - Key Components:  
    - EC2 Instances: Virtual servers.  
    - EBS (Elastic Block Store): Persistent block storage for EC2.  
    - ELB (Elastic Load Balancer): Distributes traffic across instances.  
    - Auto Scaling Groups: Automatically adjusts the number of instances based on demand.  

- EC2 User Data:  
  - Used to bootstrap instances by running scripts at the first launch.  
  - Automates tasks like:  
    - Installing OS updates.  
    - Installing software.  
    - Downloading files from the internet.  
  - Note: The user data script runs only once during the initial startup.  

---  

These concepts build a foundational understanding of AWS security (IAM) and compute services (EC2).