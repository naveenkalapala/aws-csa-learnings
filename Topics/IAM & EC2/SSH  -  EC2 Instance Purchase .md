Day 4: AWS Learning Notes

---

11. SSH Summary Table

| OS/Tool      | SSH | PuTTY | EC2-Connect |
|------------------|---------|-----------|-----------------|
| Mac          | ✅      | ❌        | ✅              |
| Linux        | ✅      | ❌        | ✅              |
| Windows < 10 | ❌      | ✅        | ✅              |
| Windows ≥ 10 | ✅      | ✅        | ✅              |

---

12. SSH Connection Methods

- Mac/Linux:  
  
  ssh -i "key_pair.pem" ec2-user@<EC2-Public-IP>
  

- Windows (<10):  
  - Use PuTTY. Convert `.pem` to `.ppk` using PuTTYgen.  
  - Connect via PuTTY with the `.ppk` key.  

- Windows (≥10):  
  - SSH available natively in PowerShell/Command Prompt.  
  - Same command as Mac/Linux.  

- EC2-Connect:  
  - AWS Console → EC2 → Select Instance → Connect → EC2 Instance Connect (Browser-based SSH).  

---

13. Attaching IAM Role to EC2 Instances

- Purpose: Allows EC2 to interact with AWS services without storing credentials.  
- Steps:  
  1. Create an IAM Role with the required permissions (e.g., S3 access).  
  2. Attach the IAM Role during EC2 instance creation or later via the console.  
  3. Use the AWS CLI or SDKs without configuring credentials.  

- Example Command (S3 Access):  
  
  aws s3 ls
  

---

14. EC2 Instance Purchase/Lauch Types

1. On-Demand Instances:  
   - Pay-as-you-go pricing.  
   - Ideal for short-term, unpredictable workloads.  

2. Reserved Instances (RI):  
   - 1 to 3-year commitment with up to 75% discount.  
   - Types:  
     - Standard RI: For steady-state workloads.  
     - Convertible RI: Flexible instance types.  
     - Scheduled RI: Reserved for specific time slots.  

3. Spot Instances:  
   - 90% cheaper than On-Demand.  
   - Ideal for fault-tolerant, flexible workloads.  
   - Can be terminated by AWS at any time.  

4. Dedicated Hosts:  
   - Physical servers exclusively allocated to you.  
   - Useful for compliance or software licensing.  

5. Dedicated Instances:  
   - Virtual instances on dedicated hardware.  
   - More isolated than shared hardware but not tied to specific servers.  

---

15. EC2 Summary

- EC2 Instance: Combination of AMI + Instance Type (CPU/RAM) + Storage.  
- Security Groups: Virtual firewall controlling traffic to/from EC2.  
- EC2 User Data: One-time bootstrap script on first boot.  
- SSH: Remote terminal access to the EC2 instance.  
- IAM Role: Grants EC2 permissions to AWS services without storing keys.  
- Purchase Options: On-Demand, Reserved, Spot, Dedicated Hosts/Instances.  

---  

This summary covers key concepts of EC2 setup, connection methods, IAM roles, and purchasing options.