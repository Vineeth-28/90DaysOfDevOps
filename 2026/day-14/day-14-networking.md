
# Day 14 – Networking Fundamentals & Hands-on Checks

## Goal
Build comfort with core networking concepts and commands used during daily troubleshooting.

---

## Quick Concepts

### OSI vs TCP/IP (in my words)
- **OSI (L1–L7):** Conceptual model to understand how data moves end-to-end.
- **TCP/IP:** Practical implementation used on real networks.

**Mapping:**
- OSI L1–L2 → TCP/IP Link
- OSI L3 → TCP/IP Internet
- OSI L4 → TCP/IP Transport
- OSI L5–L7 → TCP/IP Application

---

### Where Common Protocols Sit
- **IP:** OSI Layer 3 / TCP-IP Internet
- **TCP / UDP:** OSI Layer 4 / TCP-IP Transport
- **HTTP / HTTPS:** OSI Layer 7 / TCP-IP Application
- **DNS:** OSI Layer 7 (uses UDP/TCP at Layer 4)

---

### Real Example
- `curl https://example.com`
  - Application layer (HTTP)
  - over Transport layer (TCP)
  - over Internet layer (IP)

---

## Hands-on Checklist

### Identity
```bash
hostname -I
````

* Observed private IP assigned to the instance.

📸 Screenshot: IP address output

---

### Reachability

```bash
ping google.com -c 4
```

* Low latency and 0% packet loss observed.

---

### Path

```bash
traceroute google.com
```

* Multiple hops through ISP and backbone networks.
* Some hops timed out (ICMP blocked).

---

### Ports & Services

```bash
ss -tulpn
```

* Observed SSH listening on port 22.

---

### Name Resolution

```bash
dig google.com
```

* Domain resolved successfully to multiple IPs.

---

### HTTP Check

```bash
curl -I https://google.com
```

* Received HTTP `200 OK`.

---

### Connections Snapshot

```bash
netstat -an | head
```

* Observed LISTEN and ESTABLISHED states.

---

## Mini Task: Port Probe & Interpret

### Identified Service

* SSH listening on port **22**

### Test

```bash
nc -zv localhost 22
```

* Port is reachable.

**If unreachable:**

* Next check → `systemctl status ssh` or firewall rules.

---

## Reflection

### Fastest Signal When Something Breaks

* `ping` — quickly shows network reachability issues.

---

### Layer to Inspect Next

* **DNS failure:** Application layer (DNS) + `/etc/resolv.conf`
* **HTTP 500 error:** Application layer (service logs)

---

### Two Follow-up Checks in a Real Incident

1. `journalctl -u <service>`
2. `ss -tulpn` to confirm ports and listeners

---

