# Explore Google hacking and enumeration 
### NAME : swetha.M
### REGISTER NUMBER:212223040223
# AIM:

To use Google for gathering information and perform enumeration of targets

## STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various Google hacking keywords and enumeration tools as follows:


### Step 3:
Open terminal and try execute some kali linux commands

## Pen Test Tools Categories:  

| Operator    | Description                        | Example Usage           |
| ----------- | ---------------------------------- | ----------------------- |
| `site:`     | Search within a specific domain    | `site:example.com`      |
| `inurl:`    | Search in URL                      | `inurl:admin`           |
| `intitle:`  | Search in page title               | `intitle:"index of"`    |
| `filetype:` | Search by file type                | `filetype:pdf`          |
| `intext:`   | Search inside page text            | `intext:"confidential"` |
| `link:`     | Pages that link to a specific site | `link:example.com`      |
| `cache:`    | View cached version of a site      | `cache:example.com`     |
| `ext:`      | Same as filetype                   | `ext:xls`               |

 ## Architecture 
 ```
+----------------------+
|   Attacker / Hacker  |
|   (Browser & Google) |
+----------+-----------+
           |
           | Google Dork Queries
           v
+---------------------------+
|       Google Search       |
+---------------------------+
           |
           | Indexed Public Content
           v
+---------------------------+
|   Target Websites / Data  |
| - Leaked files            |
| - Open directories        |
| - Sensitive info          |
+---------------------------+

```

# Output:
SITE:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2a4cdb1e-bb24-40a5-bb5e-8aef6b1b7daa" />
INURL:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/350fed71-39ae-4bf3-95ca-db8c7f8dcba3" />
INTITLE:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/84e61164-08c8-48c2-ae91-7a8cb859fcaf" />
FILETYPE.PDF
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/eac9b016-f391-41a6-8613-8e0a85ee2928" />
INTEXT:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b37fd071-d9eb-4828-88be-79a05c33a79c" />
LINK:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/76a66a8c-be5e-463a-a9e4-f9d4ce585e1d" />
CACHE:
![L-3 IMG 7](https://github.com/user-attachments/assets/e4d61750-1b1e-4994-942e-dcd78251d64e)

# DNS Enumeration

<img width="1218" height="684" alt="image" src="https://github.com/user-attachments/assets/595e0b6c-01d8-4ea4-9555-5bd478bc0dec" />


## DNS Recon

| Record Type | Meaning                        | Example Output                   |
| ----------- | ------------------------------ | -------------------------------- |
| A           | Host to IPv4 address           | `example.com -> 93.184.216.34`   |
| AAAA        | Host to IPv6 address           | `example.com -> ::1`             |
| MX          | Mail server info               | `mail.example.com`               |
| NS          | Name servers                   | `ns1.example.com`                |
| TXT         | Misc data (SPF, verifications) | `v=spf1 include:_spf.google.com` |
| CNAME       | Canonical names (aliases)      | `www -> example.com`             |

## Common Tools Used (Kali Linux)

| Tool           | Description                                | Usage Example                           |
| -------------- | ------------------------------------------ | --------------------------------------- |
| `nslookup`     | DNS lookup tool (simple queries)           | `nslookup example.com`                  |
| `dig`          | DNS lookup utility (detailed)              | `dig example.com any`                   |
| `host`         | Simple DNS querying tool                   | `host example.com`                      |
| `dnsenum`      | Perl script to enumerate DNS info          | `dnsenum example.com`                   |
| `fierce`       | DNS scanner to locate non-contiguous IPs   | `fierce -dns example.com`               |
| `dnsrecon`     | Powerful DNS enumeration script            | `dnsrecon -d example.com -a`            |
| `theHarvester` | Subdomain enumeration using search engines | `theHarvester -d example.com -b google` |


## OUTPUT:

### NSLOOKUP:
<img width="928" height="857" alt="image" src="https://github.com/user-attachments/assets/ec07a6c4-f721-4384-93fe-eb07014e898d" />

### DIG:
<img width="796" height="631" alt="image" src="https://github.com/user-attachments/assets/6cb30cf2-4716-4eb9-b605-fe3f7540a1f3" />

### HOST:
<img width="765" height="636" alt="image" src="https://github.com/user-attachments/assets/25893560-1825-4bc0-8ec8-eac9d2bce5c6" />

### DNSENUM:
<img width="1218" height="684" alt="image" src="https://github.com/user-attachments/assets/595e0b6c-01d8-4ea4-9555-5bd478bc0dec" />


### FIERCE:
<img width="698" height="603" alt="image" src="https://github.com/user-attachments/assets/4048f80b-b6c9-48b8-84a1-4506f64f7c4e" />

### theHarvester:
<img width="835" height="645" alt="image" src="https://github.com/user-attachments/assets/b83263e2-7724-484b-b786-c2a42ff63c60" />

## Architecture Diagram 
```
+-------------------+        +------------------+       +------------------+
|                   |        |                  |       |                  |
|   Attacker (You)  +------->|   Target Server   +<----->+    DNS Server    |
| Kali Linux / Parrot|       | (Mail / DNS Host) |       |  (Authoritative) |
+---------+---------+        +---------+--------+       +---------+--------+
          |                            ^                          ^
          |                            |                          |
          |                            |                          |
          |           +-----------------------------+            |
          |           |      Information Tools      |            |
          |           |-----------------------------|            |
          |           | smtp-user-enum              |            |
          |           | nmap --script smtp-enum-*   |            |
          |           | dnsenum                     |<-----------+
          |           +-----------------------------+
          |
          v
+-----------------------------+
|   Output/Report             |
|  - Usernames Found          |
|  - MX Records / Zones       |
|  - Subdomains / IPs         |
+-----------------------------+

```

## dnsenum
**Purpose:** A multithreaded Perl script to enumerate information from DNS servers.

**Use case:** Performs DNS zone transfers, brute force subdomains, and gather host IPs.

```
dnsenum example.com
```

## Output:
<img width="1218" height="684" alt="image" src="https://github.com/user-attachments/assets/595e0b6c-01d8-4ea4-9555-5bd478bc0dec" />



## smtp-user-enum
**Purpose:** Standalone tool used to enumerate valid users by using the VRFY, EXPN, or RCPT TO commands.

**Use case:** Brute-forces SMTP to find users.

```
smtp-user-enum -M VRFY -U users.txt -t <target-ip>
```
  
 ## Output
  <img width="920" height="385" alt="image" src="https://github.com/user-attachments/assets/fd8013e8-c6d0-44e6-84a9-5e101b09826c" />



## nmap –script smtp-enum-users.nse <hostname>

**Purpose:** Uses smtp-enum-users NSE script to enumerate valid users on an SMTP server.

**Use case:** Helps identify email accounts on mail servers.

```
nmap -p 25 --script smtp-enum-users.nse <target-ip>
```
## OUTPUT:
<img width="932" height="205" alt="image" src="https://github.com/user-attachments/assets/57626337-5202-4fb0-9802-248fd950024f" />



## RESULT:
The Google hacking keywords and enumeration tools were identified and executed successfully
