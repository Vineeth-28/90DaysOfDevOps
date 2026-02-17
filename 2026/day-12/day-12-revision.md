
# Day 12 – Breather & Revision (Days 01–11)

## Goal
Consolidate Linux fundamentals from Days 01–11 to strengthen recall and confidence before moving ahead.

---

## 1. Mindset & Plan Review (Day 01)
- Original goal: Build strong Linux fundamentals for DevOps
- Status: On track ✅
- What’s working well:
  - Hands-on commands daily
  - Writing notes after practice
- Tweaks:
  - Spend more time on permissions (`chmod`, `chown`)
  - Reduce command memorization, increase usage in scenarios

---

## 2. Processes & Services Review (Days 04–05)

### Commands Re-run
```bash
ps aux | head
````

* Observed running system and user processes
* Noted difference between root-owned and user-owned processes

```bash
systemctl status nginx
```

* Checked service state (active/running)
* Saw main PID and worker processes

```bash
journalctl -u nginx --no-pager | tail
```

* Viewed recent logs
* Helpful for debugging startup issues

---

## 3. File Skills Practice (Days 06–11)

### Commands Practiced

```bash
mkdir test-dir
echo "revision test" >> test-dir/file.txt
ls -l test-dir/file.txt
```

```bash
chmod 644 test-dir/file.txt
```

* Owner has read/write, others read-only

```bash
cp test-dir/file.txt test-dir/file-copy.txt
```

---

## 4. Cheat Sheet Refresh (Day 03)

### 5 Commands I’d Reach for First in an Incident

1. `ps aux` – check running processes
2. `systemctl status <service>` – service health
3. `journalctl -xe` – system logs
4. `df -h` – disk usage
5. `ls -l` – permissions and ownership

---

## 5. User / Group Sanity Check (Day 09 / 11)

### Scenario

Create a test user and verify ownership.

```bash
sudo useradd testuser
id testuser
```

```bash
sudo chown testuser:testuser test-dir/file.txt
ls -l test-dir/file.txt
```

* Ownership successfully changed
* Verified using `ls -l`

---

## 6. Mini Self-Check

### Q1: Which 3 commands save you the most time right now, and why?

* `systemctl status` – instant service health
* `ls -l` – quick permission and ownership check
* `journalctl -u` – targeted service logs

---

### Q2: How do you check if a service is healthy?

```bash
systemctl status nginx
ps aux | grep nginx
journalctl -u nginx --no-pager | tail
```

---

### Q3: How do you safely change ownership and permissions?

Example:

```bash
sudo chown ubuntu:ubuntu file.txt
chmod 644 file.txt
```

* Change owner first
* Then apply least-required permissions

---

### Q4: Focus for the next 3 days

* Stronger grasp of permission numbers
* More practice with logs and services
* Start thinking in troubleshooting scenarios

---

## Key Takeaways

* Repetition builds confidence
* systemd + logs are core DevOps tools
* Permissions mistakes can break access — always verify

---

## Learn in Public

Reinforced Linux fundamentals today.
Feeling more confident with `systemctl status` and `journalctl`.

#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham

```

---

If you want, I can:
- Review this like a **mentor** before you commit
- Convert it into a **short LinkedIn/X post**
- Help you prep **Day 13** so momentum stays 🔥
```
