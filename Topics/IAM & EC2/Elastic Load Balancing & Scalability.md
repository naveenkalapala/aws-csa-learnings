Day 7 Highlights: Elastic Load Balancing & Scalability

35. Elastic Load Balancing & Scalability
- Scalability: Ability to handle increased load by adapting resources.
  - Vertical Scaling (Scale Up/Down):
    - Increasing instance size (e.g., t2.micro → t2.large).
    - Common in non-distributed systems like databases.
    - Limited by hardware constraints.
  - Horizontal Scaling (Scale Out/In = Elasticity):
    - Adding more instances to handle load.
    - Common in distributed systems like web applications.
    - Easier to implement in cloud environments.

36. High Availability & Scalability for EC2
- Vertical Scaling: Increase instance size.
- Horizontal Scaling: Add/remove instances dynamically.
  - Key Components:
    - Auto Scaling Group (ASG): Automatically scales instances based on demand.
    - Load Balancer (LB): Distributes traffic efficiently.
- High Availability:
  - Running instances in multiple Availability Zones (AZs).
  - Ensures system survives data center failures.

37. Scalability vs Elasticity
- Scalability: Ability to handle larger loads by adding resources.
  - Scale Up: Upgrade hardware (bigger instance).
  - Scale Out: Add more instances (horizontal scaling).
- Elasticity: Automatic scaling based on demand.
  - Optimizes cost & performance by matching resource allocation to load.

---

38. What is Load Balancing?
- Definition: Load balancing distributes incoming traffic across multiple EC2 instances to improve performance, availability, and reliability.

---

39. Why Use a Load Balancer?

    1. Distributes Traffic Efficiently :
            Spreads user requests across multiple backend servers (instances), preventing any single server from being overwhelmed.
    2. Improves Application Availability & Fault Tolerance :
            If one server fails, the load balancer redirects traffic to healthy instances, ensuring high availability.
    3. Enhances Performance & Scalability :
            Load balancers can direct traffic based on factors like server health, geographic location, and response time, improving user experience.
    4. Supports Auto Scaling :
            Works with Auto Scaling Groups to dynamically add or remove instances based on traffic demand.
    5. Increases Security :
            Can terminate SSL/TLS connections, offloading encryption and decryption from backend servers.
            Protects applications from DDoS attacks by controlling traffic.
    6. Enables Session Persistence :
            Directs a user’s requests to the same server during a session (useful for applications requiring stateful connections).

---

40. Types of AWS Load Balancers

        Classic Load Balancer (CLB) → Basic L4 (TCP/HTTP) balancing.
        Application Load Balancer (ALB) → L7 (HTTP/HTTPS) with advanced routing.
        Network Load Balancer (NLB) → High-performance L4 (TCP/UDP) balancing.
        Gateway Load Balancer (GLB) → Load balancing for firewalls and security appliances.
---

41. Application Load Balancer (ALB) Creation
- Step 1: Open AWS EC2 → Load Balancers → Create Load Balancer.  
- Step 2: Choose Application Load Balancer (ALB).  
- Step 3: Configure Listeners (HTTP/HTTPS).  
- Step 4: Choose Availability Zones & VPC.  
- Step 5: Create a Target Group (EC2 instances to forward traffic to).  
- Step 6: Register EC2 instances to the Target Group.  
- Step 7: Set up Health Checks (to remove unhealthy instances).  
- Step 8: Configure Security Group & Routing.  
- Step 9: Review & create the ALB.  

---
