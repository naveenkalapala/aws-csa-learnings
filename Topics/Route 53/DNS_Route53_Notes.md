
# Domain Name System (DNS) & Amazon Route 53

## What is DNS?
DNS (Domain Name System) is like the internet’s phonebook.  
It translates **human-readable domain names** (like `www.example.com`) into **IP addresses** (like `192.0.2.1`) that computers use to communicate.

### DNS Hierarchical Structure
- `.com`
- `google.com`
- `www.google.com`
- `docs.google.com`

### Key DNS Terminologies
- **DNS Registrar**: Services that register domain names (e.g., Amazon Route 53, GoDaddy)
- **DNS Records**: Mapping rules (A, AAAA, CNAME, NS, etc.)
- **Zone File**: File containing DNS records
- **Name Server**: Resolves DNS queries
- **Top-Level Domain (TLD)**: `.com`, `.in`, `.org`, `.gov`, `.us`
- **Second-Level Domain (SLD)**: `google.com`, `amazon.com`

---

## Amazon Route 53

Amazon Route 53 is a **highly available and scalable DNS web service** by AWS.

### Key Features

#### 1. High Availability & Scalability
- Designed for **global reliability**
- Handles **millions of DNS queries per second**

#### 2. Domain Registration
- Register new domain names
- Transfer existing domains

#### 3. Routing Policies
- **Simple routing** → Basic DNS mapping
- **Weighted routing** → Distributes traffic based on weights
- **Latency-based routing** → Routes to AWS region with lowest latency
- **Failover routing** → Routes traffic to healthy endpoint if primary fails
- **Geolocation routing** → Routes based on geographic location

#### 4. Health Checks
- Monitors resource health
- Routes traffic away from unhealthy endpoints

#### 5. AWS Integration
- Works seamlessly with:
  - Elastic Load Balancers (ELB)
  - S3 static website hosting
  - CloudFront CDN
  - Other AWS services

---

## Summary
- **DNS** helps translate domain names into IP addresses using a hierarchical structure.
- **Amazon Route 53** provides DNS services with advanced routing, health checks, and AWS integration, ensuring high availability and scalability.
"""

