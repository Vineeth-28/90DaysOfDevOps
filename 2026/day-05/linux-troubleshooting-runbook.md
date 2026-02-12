

# 🐧 Linux Troubleshooting Runbook – Day 05
CPU, Memory, Disk, Network & Logs

## 🎯 Target Service
**Service:** ssh  
**Reason:** Core system service, always running, easy to inspect

---

## 🔹 Environment Basics

### 1. OS & Kernel info
```bash
uname -a
````

**Observation:**
Shows kernel version and architecture. Confirms OS-level context during incidents.

```bash
lsb_release -a
```

**Observation:**
Confirms Ubuntu version and release details.

---

## 🔹 Filesystem Sanity Check

### 2. Create test directory and file

```bash
mkdir /tmp/runbook-demo
cp /etc/hosts /tmp/runbook-demo/hosts-copy
ls -l /tmp/runbook-demo
```

**Observation:**
Disk is writable, permissions look normal. Basic filesystem operations working.

---

## 🔹 Snapshot: CPU & Memory

### 3. Check overall CPU & memory usage

```bash
top
```

**Observation:**
CPU usage is low, no process consuming abnormal resources.

---

### 4. Check memory usage

```bash
free -h
```

**Observation:**
Sufficient free memory available. No swap pressure observed.

---

## 🔹 Snapshot: Disk & IO

### 5. Disk usage

```bash
df -h
```

**Observation:**
Root filesystem has adequate free space. No disk-full condition.

---

### 6. Log directory size

```bash
du -sh /var/log
```

**Observation:**
Logs are within reasonable size; no uncontrolled log growth.

---

## 🔹 Snapshot: Network

### 7. Check listening ports

```bash
ss -tulpn | grep ssh
```

**Observation:**
SSH is listening on port 22 and bound correctly.

---

### 8. Connectivity check

```bash
curl -I localhost
```

**Observation:**
Local networking stack is responsive.

---

## 🔹 Logs Reviewed

### 9. SSH service logs

```bash
journalctl -u ssh -n 50
```

**Observation:**
No recent errors. Normal authentication and startup messages only.

---

### 10. System error logs

```bash
journalctl -xe
```

**Observation:**
No critical system errors related to SSH or resources.

---

## ✅ Quick Findings

* SSH service is healthy and running
* CPU and memory usage are normal
* Disk space is sufficient
* No suspicious log entries
* Network ports are correctly listening

---

## 🚨 If This Worsens (Next Steps)

1. Restart service safely

```bash
systemctl restart ssh
```

2. Increase logging verbosity for SSH and recheck logs

3. Capture deeper diagnostics:

   * `strace -p <pid>`
   * `vmstat 1 5`
   * Collect `/var/log/auth.log` for analysis

---

✍️ *End of Troubleshooting Runbook*

```

---
