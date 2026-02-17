# 👤 Day 11 – File Ownership Challenge (chown & chgrp)

This document captures hands-on practice for understanding and managing
file and directory ownership in Linux using `chown` and `chgrp`.

---

## 🧩 Task 1: Understanding Ownership

### Command Used
```bash
ls -l ~
```

**Observation:**  
The output shows columns in the format:
```
-rw-r--r-- 1 owner group size date filename
```

- **Owner** → user who owns the file
- **Group** → group that owns the file

**Difference between owner and group:**  
- Owner has primary control over the file  
- Group allows shared access for multiple users  

---

## 🧩 Task 2: Basic chown Operations

### Create file
```bash
touch devops-file.txt
```

### Check current owner
```bash
ls -l devops-file.txt
```

### Change owner to tokyo
```bash
sudo chown tokyo devops-file.txt
ls -l devops-file.txt
```

### Change owner to berlin
```bash
sudo chown berlin devops-file.txt
ls -l devops-file.txt
```

**Observation:**  
Ownership changed successfully after each `chown` command.

---

## 🧩 Task 3: Basic chgrp Operations

### Create file
```bash
touch team-notes.txt
```

### Check current group
```bash
ls -l team-notes.txt
```

### Create group
```bash
sudo groupadd heist-team
```

### Change file group
```bash
sudo chgrp heist-team team-notes.txt
ls -l team-notes.txt
```

**Observation:**  
Group ownership updated without changing the file owner.

---

## 🧩 Task 4: Change Owner & Group Together

### Create file
```bash
touch project-config.yaml
```

### Change owner and group
```bash
sudo chown professor:heist-team project-config.yaml
ls -l project-config.yaml
```

---

### Create directory
```bash
mkdir app-logs
```

### Change owner and group
```bash
sudo chown berlin:heist-team app-logs
ls -ld app-logs
```

**Observation:**  
`chown owner:group` modifies both ownership fields in one command.

---

## 🧩 Task 5: Recursive Ownership

### Create directory structure
```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

### Create group
```bash
sudo groupadd planners
```

### Change ownership recursively
```bash
sudo chown -R professor:planners heist-project/
```

### Verify
```bash
ls -lR heist-project/
```

**Observation:**  
All files and subdirectories inherited the new owner and group.

---

## 🧩 Task 6: Practice Challenge

### Create users (if not already present)
```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m nairobi
```

### Create groups
```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

### Create directory and files
```bash
mkdir bank-heist
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

### Set ownership
```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
sudo chown berlin:tech-team bank-heist/blueprints.pdf
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

### Verify
```bash
ls -l bank-heist/
```

**Observation:**  
Each file now has different owners and groups as required.

---

## 📁 Files & Directories Created
- devops-file.txt
- team-notes.txt
- project-config.yaml
- app-logs/
- heist-project/
- bank-heist/

---

## 🔧 Commands Used
- ls -l
- touch
- mkdir / mkdir -p
- chown
- chown -R
- chgrp
- groupadd
- useradd

---

## 📘 What I Learned
- File ownership controls **who** can access files
- `chown` can change both owner and group together
- Recursive ownership (`-R`) is essential for directories
- Ownership issues are common causes of permission errors

---

## 🛠️ Troubleshooting Notes
- **Permission denied?** → use `sudo` with chown/chgrp
- **Group not found?** → create it using `groupadd`
- **User not found?** → create it using `useradd`
- **Changes not applied?** → verify using `ls -l`

✍️ *End of Day 11*
