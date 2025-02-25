# PiHole-DNS

## About This Project:

The Pi-hole® is a DNS sinkhole running on a Raspberry Pi 5 within my private home lab network. This project leverages Pi-hole to block ads, trackers, and malicious domains at the network level, enhancing privacy and security for all connected devices.

## Features:

+ __Real-time Query Logging__: Displays a live feed of DNS queries processed by Pi-hole.
+ __Ad-Blocking Status__: Indicates whether a query was blocked or permitted.
+ __Client Identification__: Shows the IP address of the device making each query.
+ __DNS Response Details__: Provides information about the reply from the DNS server (IP, CNAME, NODATA).
+ __Pi-hole System Status__: Displays the active status, load, memory usage, and temperature.
+ __Navigation Menu__: Allows access to various Pi-hole settings and logs.
+ __Search and Filtering__: Enables searching and filtering of the query log by type, domain, or client.

## How It Works:

### 1. Blocklists:
- Pi-hole uses blocklists (also called "gravity" lists) as its core mechanism for blocking unwanted domains.
- These lists are text files containing domain names that Pi-hole should block.
- They often include advertising servers, tracking domains, malware sites, or specific domains like `facebook.com` that you want to block.

### 2. Gravity Update:
- Pi-hole periodically updates its gravity database by downloading blocklists from their sources.
- This keeps the blocklists up-to-date with the latest known unwanted domains.

### 3. DNS Query Interception:
- When a device on your network makes a DNS query (e.g., trying to access `facebook.com`), Pi-hole intercepts it.

### 4. Blocklist Lookup:
- Pi-hole checks the requested domain (`facebook.com` in this example) against its gravity database (the compiled blocklists).

### 5. Blocking Decision:
- **If `facebook.com` is found in the blocklist:**
  - Pi-hole marks it as a blocked domain.
  - It prevents the query from being forwarded to the upstream DNS server.
  - It returns a "null" response (typically `0.0.0.0`) or redirects to a local sinkhole.
  - The Pi-hole log records that the domain was blocked by gravity.
- **If `facebook.com` is NOT in the blocklist:**
  - Pi-hole considers it a permitted domain.
  - The query is forwarded to the upstream DNS server for resolution.

### 6. Action Taken:
- Because `facebook.com` was on the blocklist, any device trying to connect to it is unable to.

### 7. Logging:
- Pi-hole logs all DNS queries, including blocked ones.
- You can view these logs to analyze which domains are being blocked and which devices are making the requests.

## Setting Up PiHole:
