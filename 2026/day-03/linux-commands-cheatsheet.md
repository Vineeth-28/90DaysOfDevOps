# 🐧 Linux Commands Cheat Sheet (DevOps)

A quick-reference command toolkit for daily Linux troubleshooting.

---

## 🔹 Process Management

- `ps aux` → List all running processes
- `ps -ef` → Full process list with parent-child relation
- `top` → Real-time CPU & memory usage
- `htop` → Interactive process viewer (if installed)
- `pidof <process>` → Get PID of a process
- `kill <PID>` → Gracefully stop a process
- `kill -9 <PID>` → Force kill a stuck process
- `nice -n 10 <cmd>` → Start process with priority
- `renice -n -5 <PID>` → Change priority of running process

---

## 🔹 File System & Disk

- `ls -lah` → List files with permissions & sizes
- `pwd` → Show current directory
- `cd <dir>` → Change directory
- `du -sh <dir>` → Check directory size
- `df -h` → Check disk space usage
- `stat <file>` → Detailed file information
- `find /path -name file` → Search files
- `chmod 755 <file>` → Change file permissions
- `chown user:group <file>` → Change file ownership

---

## 🔹 Logs & Monitoring

- `tail -f <file>` → Follow log file in real time
- `less <file>` → Read large files safely
- `journalctl -u <service>` → View service logs
- `journalctl -xe` → View recent system errors
- `grep "error" <file>` → Search text in logs

---

## 🔹 Networking & Connectivity

- `ping <host>` → Check network connectivity
- `ip addr` → View IP addresses
- `ss -tulnp` → Check listening ports
- `curl <url>` → Test HTTP endpoints
- `dig <domain>` → DNS lookup
- `netstat -anp` → Network connections (legacy)

---

## 🔹 System & Hardware

- `uptime` → System running time & load
- `free -h` → Memory usage
- `uname -a` → Kernel & OS details
- `whoami` → Current user
- `history` → Command history

---

✍️ *End of Cheat Sheet*
