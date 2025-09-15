Day 8: Auto Scaling Groups & Scaling Strategies  

42. Auto Scaling Groups (ASG)
- Definition:  
  An Auto Scaling Group (ASG) is a collection of Amazon EC2 instances that automatically adjust in number based on demand.  
- ASG Features:  
  ✅ Health Checks → Replaces unhealthy instances automatically.  
  ✅ Automatic Scaling → Adds/removes instances as demand changes.  
  ✅ Load Balancer Integration → Registers new instances automatically.  
  ✅ Cost Optimization → Ensures only the required instances run.  

🌟 ASG Goals:  
🔹 Scale Out: Add EC2 instances when load increases.  
🔹 Scale In: Remove EC2 instances when load decreases.  
🔹 Min & Max Instances: Ensures a fixed number of instances always run.  
🔹 High Availability: Distributes instances across multiple AZs.  

---

43. Created ASG for Hands-on Practice  
- Steps involved in creating an ASG:  
  1️⃣ Define Launch Template (Instance type, AMI, Security Group).  
  2️⃣ Set Desired Capacity, Min & Max instances.  
  3️⃣ Enable Health Checks & Load Balancer Integration.  
  4️⃣ Configure Scaling Policies (Manual/Dynamic/Scheduled).  

---

44. ASG Scaling Strategies  
Auto Scaling in AWS has four main strategies:  

1️⃣ Manual Scaling
- Manually update ASG size (increase or decrease EC2 instances).  

2️⃣ Dynamic Scaling (Auto-Scaling based on demand)
- Adjusts capacity in response to real-time CloudWatch Alarms.  
- Types of Dynamic Scaling:  
  - 🔹 Simple / Step Scaling  
    - Example: CPU > 80% → Add 2 instances  
    - Example: CPU < 30% → Remove 1 instance  
  - 🔹 Target Tracking Scaling  
    - Example: Maintain ASG CPU usage at ~40% automatically.  
  - 🔹 Scheduled Scaling  
    - Example: Increase instances to 10 at 5 PM on Fridays (Predictable usage patterns).  
  - 🔹 Predictive Scaling  
    - Uses ML to predict future traffic and adjust instances accordingly.  
    - Useful for predictable workloads (e.g., daily peak traffic).  

---

45. Comparing Cloud Concepts  

- High Availability → Ensuring applications stay online by running in multiple Availability Zones (AZs).  
- Scalability → Expanding or reducing resources based on demand.  
- Vertical Scaling → Increasing the power of a single instance (e.g., upgrading from t2.micro to t2.large).  
- Horizontal Scaling → Adding more instances instead of upgrading one.  
- Elasticity → Automatically adjusting the number of instances based on load.  
- Agility → Quickly launching, managing, and scaling resources as needed.  

---

46. ELB vs. ASG  

- Elastic Load Balancer (ELB) → Distributes traffic to multiple servers, ensuring no single server is overloaded.  
  - Supports multiple Availability Zones.  
  - Types: ALB (L7 HTTP), NLB (L4 TCP), CLB (legacy).  
  - Directs traffic only to healthy instances.  

- Auto Scaling Group (ASG) → Adjusts the number of EC2 instances based on demand.  
  - Can add or remove instances automatically.  
  - Types of scaling: Manual, Dynamic, Scheduled.  
  - Replaces unhealthy instances to maintain performance.  


Key Takeaways
✅ ASGs ensure high availability & cost efficiency by automatically scaling EC2 instances.  
✅ Scaling strategies help optimize performance: Manual, Dynamic, Scheduled, Predictive.  
✅ Load Balancers (ELB) work with ASG to distribute traffic across multiple AZs.  
✅ Elasticity = Auto Scaling → Scale in/out automatically based on demand.  

