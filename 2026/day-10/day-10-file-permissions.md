# 🔐 Day 10 – File Permissions & File Operations Challenge

This document captures hands-on practice with Linux file creation, reading,
and permission management using real commands.

---

## 🧩 Task 1: Create Files

### Commands Used
```bash
touch devops.txt
echo "This file contains DevOps notes" > notes.txt
vim script.sh
```

**Content added in `script.sh`:**
```bash
echo "Hello DevOps"
```

### Verification
```bash
ls -l devops.txt notes.txt script.sh
```

**Observation:**  
All files were created successfully. By default, files do not have execute (`x`)
permission.

---

## 🧩 Task 2: Read Files

### Commands Used
```bash
cat notes.txt
vim -R script.sh
head -n 5 /etc/passwd
tail -n 5 /etc/passwd
```

**Observation:**  
- `cat` displays full file content  
- `vim -R` opens a file in read-only mode  
- `head` and `tail` are useful for inspecting large system files  

---

## 🧩 Task 3: Understand Permissions

Permission format: `rwxrwxrwx` → owner | group | others  

- r = read (4)
- w = write (2)
- x = execute (1)

### Check permissions
```bash
ls -l devops.txt notes.txt script.sh
```

**Observation:**  
- `devops.txt` → read & write for owner, read-only for group/others  
- `notes.txt` → read & write for owner  
- `script.sh` → not executable initially  

**Conclusion:**  
Only files with execute (`x`) permission can be run as programs.

---

## 🧩 Task 4: Modify Permissions

### Make script executable
```bash
chmod +x script.sh
ls -l script.sh
./script.sh
```

**Result:**
```text
Hello DevOps
```

---

### Make devops.txt read-only
```bash
chmod a-w devops.txt
ls -l devops.txt
```

---

### Set notes.txt permission to 640
```bash
chmod 640 notes.txt
ls -l notes.txt
```

---

### Create directory with 755 permissions
```bash
mkdir project
chmod 755 project
ls -ld project
```

**Observation:**  
Permission changes were applied successfully and reflected via `ls -l`.

---

## 🧩 Task 5: Test Permissions

### Try writing to read-only file
```bash
echo "test line" >> devops.txt
```

**Result:**
```text
Permission denied
```

---

### Try executing file without execute permission
```bash
chmod -x script.sh
./script.sh
```

**Result:**
```text
Permission denied
```

---

## 📁 Files Created
- devops.txt
- notes.txt
- script.sh
- project/ (directory)

---

## 🔧 Commands Used
- touch
- echo > file
- vim / vim -R
- cat
- head
- tail
- chmod
- ls -l
- mkdir

---

## 📘 What I Learned
- Files need execute (`x`) permission to run
- Numeric permissions (755, 640) are easier to reason about
- `ls -l` is the first command to debug permission issues
- Permission errors clearly explain what is missing

---

## 🛠️ Troubleshooting Notes
- **Permission denied while writing?** → check write (`w`) permission
- **Script not running?** → check execute (`x`) permission
- **Unsure who has access?** → inspect owner, group, and others via `ls -l`

✍️ *End of Day 10*
