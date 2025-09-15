# How DNS Works  

When you type a domain like **`example.com`** in your browser, the Domain Name System (DNS) translates it into the server’s IP address (e.g., **9.10.11.12**). 

This process happens in multiple steps:

---

## Step 1: Browser Request
- You enter **example.com** in the **Web Browser**.  
- Browser checks its **cache (TTL)** first:
  - If cached, it returns the IP directly.  
  - If not, it queries the **Local DNS Server**.

---

## Step 2: Local DNS Server
- Assigned and managed by:
  - Your **ISP (Internet Service Provider)**, or  
  - Your **Company’s network**.  
- If the answer is not cached locally, it queries higher-level DNS servers.

---

## Step 3: Root DNS Server
- Managed by **ICANN**.  
- The local DNS asks: *“Where can I find `.com`?”*  
- Root DNS responds with the **TLD (.com) nameserver** address (e.g., `1.2.3.4`).

---

## Step 4: TLD DNS Server (.com)
- Managed by **IANA (branch of ICANN)**.  
- The local DNS asks: *“Where is `example.com`?”*  
- TLD server responds with the **Authoritative (SLD) DNS server** for `example.com` (e.g., `5.6.7.8`).

---

## Step 5: SLD (Authoritative) DNS Server
- Managed by the **Domain Registrar** (e.g., Amazon Registrar, GoDaddy).  
- The local DNS asks: *“What is the IP of `example.com`?”*  
- Authoritative server responds with **IP: 9.10.11.12**.

---

## Step 6: Response to Browser
- Local DNS caches the result for the configured **TTL** (Time To Live).  
- Returns the IP **9.10.11.12** to the browser.  
- Browser then contacts the **Web Server** (example.com).

---

## Summary
- **Root DNS** → Knows TLDs (.com, .org, .net, …)  
- **TLD DNS** → Knows authoritative servers for domains under that TLD  
- **SLD/Authoritative DNS** → Provides the actual IP address of the domain  
- **Local DNS** → Acts as a middleman + caches results  
- **Browser** → Uses the IP to load the website  

---

👉 This process ensures that human-readable names (**example.com**) are resolved into machine-readable IPs (**9.10.11.12**).

"""
