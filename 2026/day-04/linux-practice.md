
# 🐧 Linux Practice – Processes & Services (Day 04)

This practice log captures the basic Linux commands I ran to understand
processes, systemd services, and logs on my system.

---

## 🔹 Process Checks

### 1. List running processes
```bash
ps aux | head -10
````

**Observation:**
Displays all running processes with CPU and memory usage. Useful to quickly
identify resource-heavy processes.

---

### 2. Real-time process monitoring

```bash
top
```

**Observation:**
Shows live CPU, memory usage, load average, and running processes. Helps during
performance troubleshooting.

---

## 🔹 Service Checks (systemd)

### 3. Check status of SSH service

```bash
systemctl status ssh
```

**Observation:**

* Service is active and running
* Shows main PID, uptime, and recent logs
* Confirms whether the service is healthy

---

### 4. List running systemd services

```bash
systemctl list-units --type=service --state=running
```

**Observation:**
Lists all currently running services managed by systemd.

---

## 🔹 Log Checks

### 5. View logs for SSH service

```bash
journalctl -u ssh --no-pager | tail -20
```

**Observation:**
Shows recent SSH authentication and service activity. Useful for debugging
connection issues.

---

### 6. View recent system errors

```bash
journalctl -xe
```

**Observation:**
Displays recent system warnings and errors with helpful diagnostic messages.

---

## 🔹 Mini Troubleshooting Flow (Example)

**Scenario:** SSH service not responding

1. Check service status

```bash
systemctl status ssh
```

2. Restart the service

```bash
systemctl restart ssh
```

3. Check logs for errors

```bash
journalctl -u ssh
```

4. Check system resource usage

```bash
top
```

**Result:**
Service health, logs, and system load clearly indicate whether the issue is
service-related or resource-related.

---

✍️ *End of Practice Log*

```

---

