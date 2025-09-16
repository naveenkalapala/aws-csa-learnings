#  DNS TTL in Route 53

##  What is TTL?

* **TTL (Time To Live)** is the amount of time (in seconds) that a DNS response is cached by a client or DNS resolver.
* Example:

  ```
  myapp.example.com → 203.0.113.25 (A record, TTL = 300 seconds)
  ```

  * The client will cache this answer for **300 seconds**.
  * Any repeated requests during this time will use the cached result (no new DNS query needed).

**Purpose:** Reduce DNS query traffic and improve performance since DNS records don’t change frequently.

---

##  TTL Trade-offs

* **High TTL (e.g., 24 hours)**
  ✅ Less traffic on Route 53 (cost-efficient).
  ❌ Slower to propagate updates (takes 24h for all caches to expire).

* **Low TTL (e.g., 60 seconds)**
  ✅ Faster propagation of changes (updates take effect within a minute).
  ❌ More DNS queries to Route 53 (higher traffic and cost).

### 📌 Best Practice

* If you **plan to update a record**:

  1. Lower the TTL to a small value (e.g., 60 seconds).
  2. Wait until caches expire with the new low TTL.
  3. Update the DNS record.
  4. After propagation, increase the TTL again.

This balances **update speed** and **query efficiency**.

---

##  TTL Demonstration in Route 53

1. **Create a Record**

   * Example: `api.naveenkalapala.com` → points to an EC2 instance (IP).
   * Set TTL = **120 seconds (2 minutes)**.

2. **Verify Record**

   * Browser (e.g., Chrome) resolves the domain correctly.
   * `nslookup` confirms the IP address.
   * `dig` shows TTL in seconds (e.g., 115 → decreasing to 98 as cache time reduces).

3. **Update Record**

   * Change the record to a new IP (different region).
   * Cached responses keep showing the **old IP** until TTL expires.
   * After TTL expiration, new queries return the updated IP.

4. **Propagation Example**

   * TTL = 120 seconds.
   * If record is updated at T=0 but client still has 66s left in cache,
     → Old IP is used for 66 more seconds.
   * After TTL expires, client queries Route 53 again and gets the new IP.

---

## Key Takeaways

* TTL defines **how long DNS responses are cached**.
* **High TTL** = better performance, slower updates.
* **Low TTL** = faster updates, more DNS traffic.
* Strategy: **lower TTL before planned changes, raise it back afterward**.
* TTL is required for all DNS records **except Alias records** (special AWS records).

---

# Route 53 TTL Explained with Example

## Scenario

You have a web application hosted at **`myapp.example.com`**.
The DNS record is an **A record** pointing to your server’s IP address:

```
myapp.example.com → 203.0.113.25
TTL = 300 seconds (5 minutes)
```

---

## How TTL Works (Step by Step)

### 1. First Request

* A client (say a user in Chrome) requests **myapp.example.com**.
* The DNS resolver asks Route 53 and gets:

  * **IP = 203.0.113.25**
  * **TTL = 300 seconds**
* The resolver caches this result for **5 minutes**.
* User’s browser connects to the web server at `203.0.113.25`.

---

### 2. Subsequent Requests (Within TTL)

* The same client makes another request **after 2 minutes**.
* Instead of asking Route 53 again, the resolver uses the **cached IP**.
* This reduces DNS traffic and speeds up the response.
* TTL countdown continues (e.g., now 180 seconds left).

---

### 3. Changing the Record

Suppose you deploy a new version of your app on another server in a different region:

```
myapp.example.com → 198.51.100.45
```

You update the A record in Route 53, but…
⚠️ Clients who still have the old IP cached (203.0.113.25) will keep using it **until their 300s TTL expires**.

---

### 4. Propagation Delay

* At the time of update, a client may still have **200s left in cache**.
* That client will continue hitting the **old server** for 200s.
* After TTL expires, the resolver queries Route 53 again and receives the **new IP (198.51.100.45)**.
* From that point on, the client connects to the new server.

---

## TTL Trade-off Example

* **If TTL = 24 hours**

  * Clients cache results for a full day.
  * Updates (like moving traffic to a new server) may take **up to 24 hours** to fully propagate.

* **If TTL = 60 seconds**

  * Clients re-query every minute.
  * Updates propagate in about **1 minute**.
  * But this generates a lot more DNS traffic to Route 53 (higher cost).

---

## ✅ Best Practice Example

Let’s say you plan to **migrate servers tomorrow**:

1. Today: Lower the TTL from 300s → 60s.
2. Wait at least 5 minutes (old TTL) so everyone caches the new short TTL.
3. Migrate the server and update DNS record.
4. Clients switch over within \~1 minute.
5. After migration, increase TTL back to 300s or higher to reduce query load.

---

## 🔎 Verification with Tools

* Run `nslookup myapp.example.com` → shows the IP.
* Run `dig myapp.example.com` → shows the IP + TTL countdown.
  Example:

  ```
  ;; ANSWER SECTION:
  myapp.example.com.  115 IN A 203.0.113.25
  ```

  * Here TTL = 115 seconds (will keep decreasing until 0).

---

 In summary:

* **TTL is the timer for cached DNS answers.**
* **Low TTL** → faster updates but more DNS traffic.
* **High TTL** → fewer queries but slower updates.

---
