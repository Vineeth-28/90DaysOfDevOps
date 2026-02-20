
# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

## 📌 Objective
Understand the core networking fundamentals every DevOps engineer must know:
- DNS resolution
- IPv4 addressing
- CIDR & subnetting
- Ports and services

---

# 🔹 Task 1: DNS – How Names Become IPs

## What happens when you type `google.com` in a browser?

1. The browser checks its local DNS cache.
2. If not found, it queries a DNS resolver (ISP or public DNS like 8.8.8.8).
3. The resolver contacts Root → TLD → Authoritative DNS servers.
4. The authoritative server responds with the IP address.
5. The browser connects to that IP using HTTP/HTTPS.

---

## DNS Record Types

- **A** – Maps domain to an IPv4 address.
- **AAAA** – Maps domain to an IPv6 address.
- **CNAME** – Alias record pointing to another domain.
- **MX** – Specifies mail server for a domain.
- **NS** – Specifies authoritative name servers.

---

## Command Output – `dig google.com`

Example:

```

;; ANSWER SECTION:
google.com.    118    IN    A    142.250.183.14

```

- **A Record IP:** 142.250.183.14  
- **TTL:** 118 seconds  

---

# 🔹 Task 2: IP Addressing

## What is an IPv4 address?

An IPv4 address is a 32-bit numerical address written in dotted decimal format.

Example:
```

192.168.1.10

```

It contains:
- Network portion
- Host portion

---

## Public vs Private IP

| Type        | Description | Example |
|------------|------------|----------|
| Public IP  | Accessible over internet | 8.8.8.8 |
| Private IP | Used inside internal networks | 192.168.1.10 |

---

## Private IP Ranges

- 10.0.0.0 – 10.255.255.255
- 172.16.0.0 – 172.31.255.255
- 192.168.0.0 – 192.168.255.255

---

## Command Output – `ip addr show`

Example:

```

inet 172.31.24.216/20

```

This is a **private IP** (172.16–172.31 range).

---

# 🔹 Task 3: CIDR & Subnetting

## What does `/24` mean?

In `192.168.1.0/24`:

- First 24 bits = Network bits
- Remaining 8 bits = Host bits
- Subnet Mask = 255.255.255.0

---

## Usable Hosts

| CIDR | Total IPs | Usable Hosts |
|------|-----------|--------------|
| /24  | 256       | 254          |
| /16  | 65536     | 65534        |
| /28  | 16        | 14           |

(Usable Hosts = Total IPs − 2)

---

## Why do we subnet?

We subnet to:
- Reduce broadcast traffic
- Improve performance
- Increase security
- Organize infrastructure
- Efficiently manage IP addresses

---

## CIDR Table

| CIDR | Subnet Mask       | Total IPs | Usable Hosts |
|------|-------------------|-----------|--------------|
| /24  | 255.255.255.0     | 256       | 254          |
| /16  | 255.255.0.0       | 65536     | 65534        |
| /28  | 255.255.255.240   | 16        | 14           |

---

# 🔹 Task 4: Ports – The Doors to Services

## What is a port?

A port is a logical communication endpoint that allows multiple services to run on a single IP address.

Ports help direct traffic to the correct application.

---

## Common Ports

| Port | Service |
|------|----------|
| 22   | SSH |
| 80   | HTTP |
| 443  | HTTPS |
| 53   | DNS |
| 3306 | MySQL |
| 6379 | Redis |
| 27017| MongoDB |

---

## Command Output – `ss -tulpn`

Example:

```

tcp   LISTEN  0  128  0.0.0.0:22      users:(("sshd"))
tcp   LISTEN  0  128  0.0.0.0:80      users:(("nginx"))

```

Matched:
- Port 22 → SSH
- Port 80 → Nginx (HTTP)

---

# 🔹 Task 5: Putting It Together

## curl http://myapp.com:8080 – What happens?

- DNS resolves `myapp.com` to an IP.
- TCP connection is established.
- Request goes to port 8080.
- Application responds with HTTP data.

---

## App can't reach DB at 10.0.1.50:3306 – What to check?

- Is the IP reachable?
- Is port 3306 open (firewall/security group)?
- Is MySQL running?
- Are both systems in same VPC/subnet?

---

# 📚 What I Learned

1. DNS converts domain names into IP addresses.
2. CIDR defines network size and host capacity.
3. Ports allow multiple services to operate on one IP.

