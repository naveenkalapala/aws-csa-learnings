# Routing Policies in Route 53

Amazon Route 53 is a **highly available and scalable DNS service**.
A **routing policy** in Route 53 defines *how* DNS responds to queries.

Important clarification:

* Do **not** confuse DNS routing with network or load balancer routing.
* **DNS does not route traffic itself**. It only responds to queries with endpoints (IP addresses or domain names).
* Once the client receives the DNS response, it communicates directly with the endpoint (e.g., web server, ELB, S3).

Essentially, DNS is about **translating hostnames into endpoints**, not carrying traffic.

---

# 📌 Supported Routing Policies in Route 53

Route 53 supports several routing policies:

* **Simple**
* **Weighted**
* **Failover**
* **Latency-based**
* **Geolocation**
* **Multivalue Answer**
* **Geoproximity** (via Route 53 Traffic Flow)

We will go through each in turn.

---

## 1. Simple Routing Policy


The **Simple Routing Policy** is the most basic routing option in Route 53. It maps a single DNS name (like `www.example.com`) to a single resource, such as an EC2 instance, ELB, or IP address.

### How It Works

* When a client queries the DNS name (like `www.example.com`), Route 53 responds with the IP address from the record.
* You can provide multiple IPs in the same record set. If multiple values are returned, the client randomly selects one.
* With **alias records**, you can map directly to AWS resources (e.g., ELB, S3 website, CloudFront), but only **one resource target** is allowed.

**Limitation:** Does **not support health checks** (except if used with multiple records manually).

---

### Use Cases

* When you only have **one web server or resource**.
* When you don’t need advanced routing logic.

---

### Hands-On Example: Creating a Simple Routing Policy

1. Go to the Route 53 console.
2. Create an A record named `simple.naveen.com`.
3. Point it to an instance in `ap-southeast-1`.
4. Set a **low TTL** (e.g., 20 seconds).
5. Choose **Simple Routing Policy** and save.

✅ Testing with browser:
Visiting `simple.naveen.com` → returns *“Hello World from my instance in ap-southeast-1b.”*

✅ Testing with Terminal :

```bash
dig simple.naveen.com
```

* Returns the A record with TTL = 20s.
* Points to the correct IP.

---

### Editing the Record for Multiple IPs

* Add another IP (e.g., one in `us-east-1`).
* After TTL expires, Route 53 returns **two IPs**.
* Clients now have \~50% chance of using either IP.

Verify with `dig` again → two IPs should be returned.
Refreshing the browser shows connections to either server after TTL expiration.

---

### Key Takeaways for Simple Routing

* **DNS-level response, not traffic routing.**
* Routes to one or multiple IPs; clients choose randomly when multiple are present.
* Alias records → only **one AWS resource target**.
* TTL defines how long DNS responses are cached before clients query again.

---

## 2. Weighted Routing Policy

The **Weighted Routing Policy** allows you to distribute traffic among multiple resources by assigning weights to DNS records. Each weight represents the proportion of traffic that should go to a resource.

### How It Works

* Each record in the set has a **weight** (relative number).
* Route 53 calculates traffic distribution by dividing each record’s weight by the sum of all weights.
* Example: If weights are 70, 20, 10, Route 53 will send \~70% of responses to the first resource, 20% to the second, and 10% to the third.
* Weights do **not** need to sum to 100. They are relative values.

---

### Hands-On Example: Creating a Weighted Routing Policy

* Go to Route 53 console.

* Create two A records with the same name:

```
weighted.naveen.com
```

* First record → IP of instance in ap-southeast-1, weight = 70.

* Second record → IP of instance in us-east-1, weight = 30.

* TTL = 20 seconds.

* Choose Weighted Routing Policy and save.

✅ Testing with dig:

```
dig weighted.naveen.com
```

* Returns either of the IPs, but ~70% of the time you’ll get the Singapore instance, ~30% the US one.

* Verify by running multiple queries.

### Use Cases

* Fine-grained control over **regional traffic distribution**.
* **Regional dominance tuning** (e.g., balance traffic between two regions in North America).
* **Load balancing** across multiple regions or instances.
* **Canary testing**: Send small % of users to a new version.
* **Gradual migrations**: Slowly shift traffic from one resource to another.

### Key Notes

* All records must have the **same name and type**.
* Records can be associated with **health checks**.
* Weight = 0 means no traffic goes to that resource.
* If all weights are 0 → Route 53 responds with all records equally.

---

## 3. Failover Routing Policy

The **Failover Routing Policy** is designed for **high availability and disaster recovery**. It lets you configure **active-passive failover** between resources.

### How It Works

* You define two records:

  * **Primary** (active) resource.
  * **Secondary** (passive/standby) resource.
* Route 53 monitors the primary with a **health check**.
* If the health check fails, Route 53 automatically directs queries to the secondary resource.

---

### Hands-On Example: Creating a Failover Routing Policy

* Create two A records with the same name:
* failover.naveen.com.

* Primary → IP of instance in ap-southeast-1.

* Secondary → IP of instance in us-east-1.

* Enable health check for the primary (e.g., HTTP health check on /health).

* Set routing policy to Failover → Primary = active, Secondary = passive.

✅ Testing with dig (normal):

```
dig failover.naveen.com
```

* Returns the primary instance IP (Singapore).

✅ Testing failover:

* Stop the Singapore instance OR make the health check fail.

* After a short delay, dig resolves to the US instance IP.

---

### Use Cases

* **Disaster Recovery**: Run app in one region, failover to another if the first goes down.
* **Critical workloads** where downtime must be minimized.

---

### Key Notes

* Requires **health checks**.
* Only supports **active-passive**, not active-active.

---

## 4 . Latency-Based Routing (LBR)

The **Latency-Based Routing Policy** routes traffic to the AWS region that provides the **lowest network latency** for the end user.

### How It Works

* Route 53 has data on latency between AWS regions and user locations.
* When a DNS query comes in, Route 53 responds with the resource hosted in the region that will give the best response time.
* If the closest region is unhealthy (via health checks), Route 53 can direct traffic to the next-best region.

### Hands-On Example: Creating a Latency-Based Routing Policy

* Create A records with the same name:
```
latency.naveen.com.
```

* One pointing to instance in ap-southeast-1.

* One pointing to instance in us-east-1.

* Choose Latency Routing Policy and select corresponding regions.

✅ Testing:

* From Singapore: dig latency.naveen.com → returns ap-southeast-1 IP.

* From US  → returns us-east-1 IP.

✅ Browser Test:

* When accessed from Singapore → Hello from Singapore server.

* When accessed from US → Hello from US server.

---

### Use Cases

* **Global applications** where performance matters (e.g., users in Asia go to Singapore, US users go to Virginia).
* **Improving user experience** by minimizing latency.

---

### Key Notes

* Often combined with **health checks** for resilience.
* Latency is based on AWS’s measurements, not real-time pings from clients.

---

## 5️⃣ Geolocation Routing Policy

The **Geolocation Routing Policy** routes traffic based on the **geographic location of the DNS query’s origin** (the user making the request).

### How It Works

* You define records for specific locations (e.g., North America, Europe, Germany).
* When a DNS query comes in, Route 53 looks at the user’s IP and matches it to the configured location.
* If no location matches, a **default record** can be used.

### Hands-On Example: Creating a Geolocation Routing Policy

* Create A records for geo.naveen.com.

* For Asia → IP of Singapore instance.

* For North America → IP of US instance.

* (Optional) Default location → fallback instance.

* Choose Geolocation Routing Policy and specify regions.

✅ Testing:

* From Singapore: dig geo.naveen.com → resolves to Singapore IP.

* From US: resolves to US IP.

* From Europe: if no rule, resolves to default.

### Use Cases

* **Compliance**: Ensure EU users stay in EU servers due to GDPR.
* **Localization**: Serve content in a user’s local language or currency.
* **Restricting content**: Direct certain users to specific endpoints.

---

### Key Notes

* If a user’s location isn’t explicitly defined → Route 53 uses the **default record**.
* Location can be configured at **continent, country, or state (in US)** level.

---

## 6️⃣ Geoproximity Routing Policy

The **Geoproximity Routing Policy** routes traffic based on the **location of AWS resources** and allows you to **bias traffic** toward certain resources.

### How It Works

* Requires **Route 53 Traffic Flow** (visual editor).
* You associate resources with geographic regions.
* You can apply a **bias** (positive or negative) to shift more or less traffic toward a resource.
* Example: Shift +30% more traffic to `us-east-1` even if `ca-central-1` is closer.

---

### Key Notes

* More flexible than Geolocation.
* Only available in **Traffic Flow**, not directly in simple record sets.

---

## Multivalue Answer Routing Policy

The **Multivalue Answer Routing Policy** returns **multiple healthy records** for a single query, acting as a basic load balancer.

### How It Works

* You create multiple records with the same name and type.
* Route 53 runs **health checks** on each resource.
* Up to **8 healthy records** are returned in response to a query.
* Client chooses randomly from the returned list.

### Use Cases

* **Lightweight load balancing** without using an ELB.
* Applications where you want multiple endpoints to serve traffic.

### Key Notes

* Provides simple fault tolerance via health checks.
* Not as advanced as an Application Load Balancer (ALB) or Network Load Balancer (NLB).

---

### Summary 

* **Simple** → One or multiple IPs, random selection.
* **Weighted** → Control % of traffic across resources.
* **Failover** → Active-passive disaster recovery.
* **Latency-Based** → Routes to the region with lowest latency.
* **Geolocation** → Routes based on user’s geographic origin.
* **Geoproximity** → Routes based on resource location + optional bias (Traffic Flow).
* **Multivalue Answer** → Returns multiple healthy records, basic load balancing.

---


