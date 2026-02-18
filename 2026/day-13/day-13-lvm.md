Perfect — this is a **hands-on LVM day**, and I’ll walk you like a mentor would.
Below is a **clean, copy-paste-ready `day-13-lvm.md`** that matches *exactly* what the task asks. You just need to replace device names (`/dev/sdb` or `/dev/loop0`) and add screenshots.

---

````md
# Day 13 – Linux Volume Management (LVM)

## Objective
Learn how to create, manage, extend, and mount logical volumes using LVM.

---

## Environment
- OS: Ubuntu Linux
- User: root
- Disk used: /dev/loop0 (virtual disk)

Switched to root user:
```bash
sudo -i
````

---

## Step 0: Create a Virtual Disk (No Spare Disk Scenario)

```bash
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
losetup -fP /tmp/disk1.img
losetup -a
```

📸 Screenshot: loop device creation (`/dev/loop0`)

---

## Task 1: Check Current Storage

```bash
lsblk
pvs
vgs
lvs
df -h
```

📸 Screenshot: current storage status

---

## Task 2: Create Physical Volume

```bash
pvcreate /dev/loop0
pvs
```

📸 Screenshot: physical volume created

---

## Task 3: Create Volume Group

```bash
vgcreate devops-vg /dev/loop0
vgs
```

📸 Screenshot: volume group details

---

## Task 4: Create Logical Volume

```bash
lvcreate -L 500M -n app-data devops-vg
lvs
```

📸 Screenshot: logical volume created

---

## Task 5: Format and Mount Logical Volume

```bash
mkfs.ext4 /dev/devops-vg/app-data
mkdir -p /mnt/app-data
mount /dev/devops-vg/app-data /mnt/app-data
df -h /mnt/app-data
```

📸 Screenshot: mounted filesystem

---

## Task 6: Extend the Logical Volume

```bash
lvextend -L +200M /dev/devops-vg/app-data
resize2fs /dev/devops-vg/app-data
df -h /mnt/app-data
```

📸 Screenshot: extended volume size

---

## What I Learned

1. LVM allows resizing storage without unmounting disks.
2. Logical volumes can be extended easily when free space exists in a VG.
3. `resize2fs` is required after extending an ext4 filesystem.

---

## Key Commands Summary

* `pvcreate` – initialize physical volume
* `vgcreate` – create volume group
* `lvcreate` – create logical volume
* `lvextend` – extend logical volume
* `resize2fs` – resize filesystem

---

