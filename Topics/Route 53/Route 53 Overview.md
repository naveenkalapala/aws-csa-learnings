## What is Amazon Route 53?

Amazon Route 53 is a highly available, scalable, fully managed, and **authoritative DNS** service.

- Being **authoritative** means customers can update DNS records, giving full control over DNS configurations.
- Route 53 allows clients to resolve domain names (e.g., `example.com`) to IP addresses (e.g., `54.22.33.44`), enabling direct access to resources like EC2 instances.
- Route 53 also acts as a **domain registrar**, enabling registration of domain names like `example.com`.
- It supports **health monitoring** of resources.
- Route 53 is the **only AWS service** with a **100% availability SLA**.
- The name "Route 53" refers to port 53, the standard port for DNS services.

---

## DNS Records in Route 53

 DNS records in Route 53 define and tells the DNS system how to handle requests for a domain name (like example.com).

 Think of it as small instructions stored on the Authoritative DNS Server that say:

    This domain should point to this IP.

    This subdomain should go here.

    Email for this domain should be handled there.


Each record includes:

- **Domain or subdomain name** (e.g., `example.com`)
- **Record type** (e.g., A, AAAA, CNAME, NS)
- **Record value** (e.g., IP address `12.34.56.78`)
- **Routing policy** (determines how Route 53 responds to DNS queries)
- **TTL (Time To Live)** (how long DNS resolvers cache the record)

### Common DNS Record Types

- **A Record:** Maps a hostname to an IPv4 address (e.g., `example.com` → `1.2.3.4`).
- **AAAA Record:** Maps a hostname to an IPv6 address.
- **CNAME Record:** Maps a hostname to another hostname (e.g., `www.example.com` → `example.com`).
  - **Note:** CNAMEs cannot be created for the zone apex (top-level domain like `example.com`).
- **NS Record:** Specifies the authoritative name servers for the hosted zone, controlling DNS query responses.

---

## Hosted Zones

Hosted zones are containers for DNS records defining routing for a domain and its subdomains. 

There are two types:

- **Public Hosted Zones:** 
  - Used for domains accessible from the internet.
  - Example: Resolving `application1.mypublicdomain.com` to an IP address.
- **Private Hosted Zones:** 
  - Used for domains accessible **only within your VPC**.
  - Example: `application1.company.internal` accessible only inside the corporate network.
  - Managed through private DNS records.

---

## Pricing Overview

- Hosted zones cost **$0.50 per month** each.
- Domain registration costs start at **$12 per year**.
- Route 53 is a paid service, not free.

---

## Public vs Private Hosted Zones

| Feature                | Public Hosted Zone                          | Private Hosted Zone                        |
|------------------------|--------------------------------------------|-------------------------------------------|
| Accessibility          | Queries from the public internet            | Queries only from within your VPC          |
| Use Case               | Public domain names (e.g., `example.com`)  | Private domain names (e.g., `example.internal`) |
| Example                | Browser queries to `example.com`            | EC2 instances resolving `api.example.internal` |
| DNS Resolution Example | Returns public IP (e.g., `54.22.33.44`)    | Returns private IP (e.g., `10.0.0.10`)     |

---



### Summary

- Route 53 enables DNS management and domain registration.
- It supports various DNS records and routing policies.
- Public hosted zones serve public internet queries.
- Private hosted zones serve internal VPC-only queries.
- The service provides high availability, health checks, and 100% SLA.

---

