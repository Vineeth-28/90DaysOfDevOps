
# 🧑‍💻 Day 09 – Linux User & Group Management Challenge

This document captures hands-on practice for Linux user, group, and permission management.


## 👥 Users & Groups Created

### Users
- tokyo
- berlin
- professor
- nairobi

### Groups
- developers
- admins
- project-team

---

## 🧩 Task 1: Create Users

### Commands Used
```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m professor

sudo passwd tokyo
sudo passwd berlin
sudo passwd professor
````

### Verification

```bash
cat /etc/passwd | grep -E "tokyo|berlin|professor"
ls -l /home
```

**Observation:**
Users were created successfully with home directories under `/home`.

---

## 🧩 Task 2: Create Groups

### Commands Used

```bash
sudo groupadd developers
sudo groupadd admins
```

### Verification

```bash
cat /etc/group | grep -E "developers|admins"
```

**Observation:**
Groups were created and visible in `/etc/group`.

---

## 🧩 Task 3: Assign Users to Groups

### Commands Used

```bash
sudo usermod -aG developers tokyo
sudo usermod -aG developers,admins berlin
sudo usermod -aG admins professor
```

### Verification

```bash
groups tokyo
groups berlin
groups professor
```

**Observation:**
Group membership is correctly assigned.

---

## 🧩 Task 4: Shared Directory – /opt/dev-project

### Create directory and set permissions

```bash
sudo mkdir /opt/dev-project
sudo chgrp developers /opt/dev-project
sudo chmod 775 /opt/dev-project
```

### Verification

```bash
ls -ld /opt/dev-project
```

### Test access

```bash
sudo -u tokyo touch /opt/dev-project/tokyo.txt
sudo -u berlin touch /opt/dev-project/berlin.txt
ls -l /opt/dev-project
```

**Observation:**
Both users could create files due to correct group ownership and permissions.

---

## 🧩 Task 5: Team Workspace

### Create user and group

```bash
sudo useradd -m nairobi
sudo passwd nairobi
sudo groupadd project-team
```

### Assign users to group

```bash
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
```

### Create shared directory

```bash
sudo mkdir /opt/team-workspace
sudo chgrp project-team /opt/team-workspace
sudo chmod 775 /opt/team-workspace
```

### Test access

```bash
sudo -u nairobi touch /opt/team-workspace/nairobi.txt
ls -l /opt/team-workspace
```

**Observation:**
User `nairobi` successfully created files in the shared directory.

---

## 📁 Directories Created

| Directory           | Group        | Permissions |
| ------------------- | ------------ | ----------- |
| /opt/dev-project    | developers   | 775         |
| /opt/team-workspace | project-team | 775         |

---

## 🔧 Commands Used

* useradd -m
* passwd
* groupadd
* usermod -aG
* groups
* mkdir
* chgrp
* chmod
* sudo -u
* ls -l

---

## 📘 What I Learned

* Group ownership is key for shared access
* `chmod 775` enables team collaboration safely
* `sudo -u` is very useful for permission testing
* Most permission issues are group-related, not user-related

---

## 🛠️ Troubleshooting Notes

* **Permission denied?** → check permissions with `ls -ld`
* **User can’t access directory?** → check group with `groups username`
* **Changes not reflected?** → re-login user or use `newgrp`

✍️ *End of Day 09*
