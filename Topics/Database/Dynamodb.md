What is DynamoDB?

Amazon DynamoDB is a **fully managed NoSQL database service** provided by AWS.  
It delivers **single-digit millisecond latency** at any scale and is built for high **availability**, **speed**, and **scalability**.

Key Features:
- Fully managed, **highly available** with replication across **3 AZs**
- **NoSQL** database (not relational)
- Scales to massive workloads — serverless, distributed
- Handles **millions of requests per second**, **trillions of rows**, **hundreds of TBs**
- Consistent, low-latency performance
- Integrated with **IAM** for security and access control
- **Auto-scaling** and **cost-efficient**

---

DynamoDB Architecture (Simplified)

```text
              +-----------------------+
              |   Your Application    |
              +----------+------------+
                         |
                 AWS SDK / API
                         |
              +----------v-----------+
              |   Amazon DynamoDB    |
              |   (Key-Value Store)  |
              +----------+-----------+
                         |
      +------------------+------------------+
      |                                     |
+-----v-----+                       +--------v--------+
| Partition |                       |   Global Tables  |
|   (SSD)   |                       | (Multi-Region)   |
+-----------+                       +------------------+
|  Replica  |                       |  Replica         |
+-----------+                       +------------------+
````

---

What is Amazon DAX (DynamoDB Accelerator)?

Amazon **DAX** is a **fully managed, in-memory cache** for DynamoDB, designed to speed up **read-heavy workloads** — especially when **milliseconds matter**.

* Delivers **microsecond** response times for read operations
* Caches frequently accessed items from DynamoDB in memory
* Supports operations like:

  * `GetItem`, `BatchGetItem`, `Query`, `Scan`, `UpdateItem`

---

DAX Architecture

```text
 +-------------+       +------------+       +---------------+
| Application | <---> |     DAX    | <---> |   DynamoDB    |
| (SDK Client)|       | (In-memory)|       | (Persistent DB)|
+-------------+       +------------+       +---------------+
```

---

Why Use DAX?

#Without DAX:

Each `GetItem`, `Query`, or `Scan` hits DynamoDB directly
➡ Response time: **1–10 ms**

#With DAX:

Reads served from in-memory cache
➡ Response time: **< 1 ms**

---

How DAX Works

* Application queries data (e.g., product info)
* DAX checks its cache:

  * ✅ **HIT** → Returns data from memory in microseconds
  * ❌ **MISS** → Fetches data from DynamoDB, stores it in cache, returns it

> Note: Write operations (`PutItem`, `UpdateItem`) go **directly** to DynamoDB and invalidate related cache entries.

---

When to Use DAX

| Use Case                      | Benefit                           |
| ----------------------------- | --------------------------------- |
| Product catalog or profiles   | Fast repeated reads               |
| Session or user state storage | Instant access                    |
| Gaming leaderboards           | Frequent reads, rare writes       |
| Shopping carts                | Fast retrieval + moderate updates |
| Serverless APIs               | High throughput, low latency      |
| Dynamic content               | Data that changes frequently      |

---

✅ Summary

Amazon DAX is a **drop-in cache layer** for DynamoDB that **drastically reduces latency** for **read-heavy applications** — all without managing external caching systems like Redis.

