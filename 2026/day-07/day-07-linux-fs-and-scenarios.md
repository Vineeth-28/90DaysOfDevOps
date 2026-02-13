
# 🐧 Day 07 – Linux File System Hierarchy & Scenario Practice

This document covers:
1. Linux File System Hierarchy (important directories)
2. Scenario-based troubleshooting practice (DevOps mindset)

---

## 📁 Part 1: Linux File System Hierarchy

### 🔹 / (root)
- Starting point of the Linux file system
- All directories branch from here

```bash
ls -l /
````

**Observed:** bin, etc, home, var, usr
**I would use this when:** I want to understand the overall system structure.

---

### 🔹 /home

* Home directories for normal users

```bash
ls -l /home
```

**Observed:** user directory
**I would use this when:** Working with user files, scripts, SSH keys.

---

### 🔹 /root

* Home directory for the root user

```bash
ls -la /root
```

**Observed:** hidden config files
**I would use this when:** Logged in as root for administrative tasks.

---

### 🔹 /etc

* Configuration files for system and services

```bash
ls -l /etc | head
cat /etc/hostname
```

**Observed:** hostname, ssh, system configs
**I would use this when:** Editing service or system configuration.

---

### 🔹 /var/log

* Stores log files (very important for DevOps)

```bash
ls -l /var/log
du -sh /var/log/* 2>/dev/null | sort -h | tail -5
```

**Observed:** syslog, auth.log, journal
**I would use this when:** Debugging services or production issues.

---

### 🔹 /tmp

* Temporary files (cleared on reboot)

```bash
ls -l /tmp
```

**Observed:** temp files and directories
**I would use this when:** Creating temporary test files.

---

### 🔹 /bin

* Essential system binaries

```bash
ls -l /bin | head
```

**Observed:** ls, cp, mv, cat
**I would use this when:** Running basic commands even in recovery mode.

---

### 🔹 /usr/bin

* User-level command binaries

```bash
ls -l /usr/bin | head
```

**Observed:** curl, grep, system tools
**I would use this when:** Running most CLI tools.

---

### 🔹 /opt

* Optional or third-party applications

```bash
ls -l /opt
```

**Observed:** (empty / custom apps)
**I would use this when:** Installing vendor or custom software.

---

## 🧠 Part 2: Scenario-Based Practice

### 🧪 Scenario 1: Service Not Starting

**Problem:** myapp service failed after reboot

**Step 1**

```bash
systemctl status myapp
```

**Why:** Check whether service is running, failed, or inactive.

**Step 2**

```bash
journalctl -u myapp -n 50
```

**Why:** View recent logs to identify error messages.

**Step 3**

```bash
systemctl is-enabled myapp
```

**Why:** Check if service starts automatically on boot.

**Step 4**

```bash
systemctl list-units --type=service
```

**Why:** Confirm if the service exists and is loaded.

**What I learned:** Always check status → logs → enablement.

---

### 🧪 Scenario 2: High CPU Usage

**Problem:** Server is slow

**Step 1**

```bash
top
```

**Why:** See live CPU usage and top processes.

**Step 2**

```bash
ps aux --sort=-%cpu | head -10
```

**Why:** Identify which process is consuming the most CPU.

**Step 3**

```bash
ps -p <PID> -o pid,ppid,cmd,%cpu,%mem
```

**Why:** Inspect the problematic process in detail.

**What I learned:** Always identify PID before taking action.

---

### 🧪 Scenario 3: Finding Service Logs (docker)

**Problem:** Developer asks where docker logs are.

**Step 1**

```bash
systemctl status docker
```

**Why:** Confirm service name and status.

**Step 2**

```bash
journalctl -u docker -n 50
```

**Why:** View recent logs from systemd journal.

**Step 3**

```bash
journalctl -u docker -f
```

**Why:** Follow logs in real time during troubleshooting.

**What I learned:** systemd services → journald logs.

---

### 🧪 Scenario 4: File Permission Issue

**Problem:** Script not executing (Permission denied)

**Step 1**

```bash
ls -l /home/user/backup.sh
```

**Why:** Check current permissions.

**Step 2**

```bash
chmod +x /home/user/backup.sh
```

**Why:** Add execute permission.

**Step 3**

```bash
ls -l /home/user/backup.sh
```

**Why:** Verify execute bit is set.

**Step 4**

```bash
./backup.sh
```

**Why:** Confirm script runs successfully.

**What I learned:** Scripts need execute permission to run.

---

## ✅ Final Takeaways

* Linux file system tells you **where to look**
* Logs live mainly in `/var/log` or `journalctl`
* Troubleshooting = structured steps, not guessing
* Scenarios build real DevOps confidence

✍️ *End of Day 07 Notes*

```