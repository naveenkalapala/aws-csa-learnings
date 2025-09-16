#  CNAME vs Alias in Amazon Route 53

##  What is Zone Apex?

The **Zone Apex** (also called the **root domain**) is the top-level domain without any subdomains.

### Examples:
| Domain                  | Is it Zone Apex? |
|-------------------------|------------------|
| `naveen.com`            | ✅ Yes           |
| `www.naveen.com`        | ❌ No            |
| `api.naveen.com`        | ❌ No            |

Zone apex is special because:
- It must have certain required DNS records (like `NS` and `SOA`)
- Standard DNS **does not allow** `CNAME` at the zone apex
- AWS Route 53 provides **Alias records** to work around this limitation

---

## CNAME vs Alias: Explained

### CNAME (Canonical Name Record)
- Maps a **subdomain** to **another domain or subdomain**
- Cannot be used at the **zone apex**
- Standard DNS feature (not AWS-specific)

### Alias Record (Route 53 Only)
- AWS-specific record type that **acts like a CNAME**
- **Can be used at the zone apex**
- Lets you point a domain to AWS resources like:
  - CloudFront
  - S3 Website
  - Elastic Load Balancer (ELB/ALB)
  - API Gateway
  - Route 53 record sets
- **No extra DNS query charges** when pointing to AWS services

---

## Real-World Scenario: `naveen.com`

I own the domain: `naveen.com`

I want:

1. `www.naveen.com` ➝ `api.naveen.com`
2. `naveen.com` (root) ➝ AWS CloudFront or ELB

### ✅ Required DNS Records:

| Record Name        | Record Type | Target                     | Notes                                     |
|--------------------|-------------|----------------------------|-------------------------------------------|
| `www.naveen.com`   | CNAME       | `api.naveen.com`           | CNAME is fine for subdomain               |
| `naveen.com`       | Alias (A)   | `d1234.cloudfront.net`     | Use Alias because CNAME not allowed here  |

---

## 📊 Comparison Table: CNAME vs Alias

| Feature                        | CNAME                     | Alias (Route 53)             |
|-------------------------------|---------------------------|------------------------------|
| Standard DNS                  | ✅ Yes                    | ❌ No (AWS-specific)         |
| Works at Zone Apex            | ❌ No                     | ✅ Yes                       |
| Points to subdomains/domains  | ✅ Yes                    | ✅ Yes                       |
| Points to AWS resources       | ⚠️ Sometimes              | ✅ Yes                       |
| Charged for DNS queries       | ✅ Yes                    | ❌ No (when to AWS services) |
| TTL customization             | ✅ Yes                    | ⚠️ No (inherits from target) |

---

## 💡 Summary

- Use **CNAME** to point **subdomains to other domains**
  - ✅ `www.naveen.com` ➝ `api.naveen.com`
- Use **Alias** to point **root domain to AWS resources**
  - ✅ `naveen.com` ➝ CloudFront, ELB, etc.
- **CNAME cannot be used at the zone apex** due to DNS protocol rules
- **Alias is AWS’s solution** to enable root domain mapping

---

## ✅ Recommended Practice (Route 53)

If you're hosting your site using AWS:

| Domain            | Record Type | Target (example)             |
|-------------------|-------------|------------------------------|
| `naveen.com`      | Alias (A)   | `d1234.cloudfront.net`       |
| `www.naveen.com`  | CNAME       | `naveen.com` or other target |

This setup ensures both your root domain and `www` subdomain are routed properly.

