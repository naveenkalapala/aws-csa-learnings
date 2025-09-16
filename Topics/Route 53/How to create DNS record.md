# How to Create DNS Records in Route 53

## Step 1: Open the Route 53 Console

* Sign in to the [AWS Management Console](https://aws.amazon.com/console/)
* Search for and open **Route 53**.

---

## Step 2: Select Your Hosted Zone

* In the left navigation pane, click **Hosted zones**.
* Select the hosted zone for your domain (e.g., `example.com`).

---

## Step 3: Create a Record

* Click the **Create record** button.

---

## Step 4: Configure the DNS Record

You will see a form with fields to fill:

* **Record name:**

  * Enter the subdomain or leave blank for the root domain.
  * Example: `www` for `www.example.com` or leave blank for `example.com`.

* **Record type:**

  * Choose the type of DNS record (e.g., A, AAAA, CNAME, MX).
  * Example: Select **A – IPv4 address**.

* **Value:**

  * Enter the value for the record, such as an IP address or hostname.
  * Example: For an A record, enter the IPv4 address like `192.0.2.1`.

* **TTL (Time to Live):**

  * Set how long DNS resolvers cache the record (default is usually fine, e.g., 300 seconds).

* **Routing policy:**

  * Choose routing policy, e.g., Simple routing for basic use.
  * Other policies include Weighted, Latency-based, Failover, etc. (usually Simple for starters).

---

## Step 5: Save the Record

* Click **Create records** to save.

---

## Example: Create an A Record for [www.example.com](http://www.example.com)

| Field          | Value         |
| -------------- | ------------- |
| Record name    | www           |
| Record type    | A             |
| Value          | 203.0.113.123 |
| TTL            | 300 (default) |
| Routing policy | Simple        |

---

## Step 6: Verify the DNS Record

* After creation, it might take some time to propagate (usually minutes).
* Use tools like `nslookup` or `dig` to verify:

```
dig www.example.com
```

---

# Summary

* Open Route 53 > Hosted Zones > Select your domain.
* Click **Create record**.
* Choose record name, type, value, TTL, and routing policy.
* Save and verify.

---

