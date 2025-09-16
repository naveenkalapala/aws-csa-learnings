# Route 53 – Health Checks

## 1. Introduction to Route 53 Health Checks

* **Purpose**: Route 53 health checks allow you to monitor the availability and performance of endpoints.
* **Scope**:

  * Primarily for **public resources** (e.g., websites, ALBs, EC2 instances).
  * Can also monitor **private resources** indirectly via CloudWatch alarms.

**Scenario Example :**
Imagine you run a global application deployed in **two AWS regions**:

* **us-east-1** → Load Balancer 1
* **eu-west-1** → Load Balancer 2

Users access the app through **mydomain.com**.

* DNS is managed by **Route 53**, which uses **latency-based routing** to send users to the nearest load balancer.
* If **eu-west-1 goes down**, health checks ensure users are **not routed** to that region.

**Solution**: Create Route 53 health checks for each region → Associate with DNS records → Automated DNS failover.

---

## 2. Types of Health Checks

Route 53 supports **three types**:

1. **Endpoint Health Checks**

   * Directly monitor endpoints (ALB, EC2, websites).
   * Example: Check `https://myapp.eu-west-1.com` for a `200 OK` response.

2. **Calculated Health Checks**

   * Combine results from multiple health checks.
   * Example: If **2 out of 3 EC2 instances are healthy**, consider the app healthy.

3. **CloudWatch Alarm Health Checks**

   * Monitor **CloudWatch alarms** (useful for **private resources**).
   * Example: Monitor EC2 CPU > 90% (private subnet) → CloudWatch alarm triggers → Health check goes unhealthy.

---

## 3. How Endpoint Health Checks Work

* AWS has **\~15 global health checkers** sending requests to endpoints.
* Endpoint is healthy if:

  * Responds with **2xx or 3xx status code**.
  * (Optional) Contains a specific string in the **first 5120 bytes** of response.

**Configuration Options:**

* **Interval**:

  * 30 sec (default, cheaper).
  * 10 sec (faster, costlier).
* **Threshold**: How many checkers must agree for the endpoint to be considered healthy (e.g., 18 of 22).
* **Protocols supported**: HTTP, HTTPS, TCP.

**Example:**

1. Create health check for ALB endpoint `myalb.eu-west-1.amazonaws.com`.
2. Set protocol: HTTPS, interval: 30 sec.
3. Configure success code: `200`.
4. Add text check for `"Welcome to MyApp"`.

If ALB doesn’t respond with **200 OK + contains string**, Route 53 marks it unhealthy and DNS stops routing traffic to it.

⚠️ **Network note**: You must allow **Route 53 health checker IPs** in your firewall/security groups.

---

## 4. Calculated Health Checks

* Used to **aggregate child health checks**.
* Logic options: **AND, OR, NOT**.
* Can combine up to **256 child health checks**.

**Example:**

* 3 EC2 instances → 3 individual health checks.
* Create a parent health check:

  * Healthy if at least **2 of 3 child checks** are healthy.
* Use Case: During **maintenance**, you can disable one child check without failing the entire parent health check.

---

## 5. Monitoring Private Resources

* **Problem**: Route 53 health checkers cannot reach private VPC resources (no internet access).
* **Solution**: Use **CloudWatch alarms** as an intermediary.

**How it works:**

1. Set up a CloudWatch metric → Example: `StatusCheckFailed` on a private EC2.
2. Create a **CloudWatch alarm** on that metric (e.g., triggers if instance status check fails).
3. Create a **Route 53 health check** linked to that CloudWatch alarm.
4. If the alarm goes into **ALARM state**, the health check becomes **unhealthy**.

** Example:**

* EC2 in private subnet → Cannot be checked directly.
* CloudWatch alarm: CPU > 90% for 5 mins → ALARM.
* Route 53 health check linked to alarm → DNS automatically stops routing to that EC2.

---

## 6. Conclusion

* **Public endpoints** → Use **Endpoint health checks**.
* **Multiple checks aggregation** → Use **Calculated health checks**.
* **Private resources** → Use **CloudWatch alarm health checks**.

Route 53 health checks = **automated DNS failover + high availability**.

---

