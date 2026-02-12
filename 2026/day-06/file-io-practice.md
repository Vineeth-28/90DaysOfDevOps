
# 📝 File I/O Practice – Day 06

This note captures basic file read/write operations using fundamental Linux commands.

---

## 🔹 Create a File

```bash
touch notes.txt
````

**What it did:**
Created an empty file named `notes.txt`.

---

## 🔹 Write and Append Text

```bash
echo "Line 1: Learning Linux file I/O" > notes.txt
```

**What it did:**
Wrote the first line to the file (overwrites existing content).

```bash
echo "Line 2: Using redirection operators" >> notes.txt
```

**What it did:**
Appended a second line to the file.

```bash
echo "Line 3: tee command appends and prints" | tee -a notes.txt
```

**What it did:**
Appended a third line while also displaying it on the terminal.

---

## 🔹 Read the File

```bash
cat notes.txt
```

**What it did:**
Displayed the full contents of the file.

```bash
head -n 2 notes.txt
```

**What it did:**
Displayed the first 2 lines of the file.

```bash
tail -n 2 notes.txt
```

**What it did:**
Displayed the last 2 lines of the file.

---

✍️ *End of File I/O Practice*

```

---

### ✅ File contents (example)
Your `notes.txt` should look like this (8–12 lines not required here since task says **write 3 lines**):

```

Line 1: Learning Linux file I/O
Line 2: Using redirection operators
Line 3: tee command appends and prints

