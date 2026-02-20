
# Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab

## 📌 Objective

Today I applied everything from Days 16–18 into real-world mini projects:

- Log rotation automation
- Server backup automation
- Cron job scheduling
- Maintenance script with logging

---

# 🔹 Task 1: Log Rotation Script

## File: log_rotate.sh

```bash
#!/bin/bash
set -euo pipefail

LOG_DIR="${1:-}"

if [ -z "$LOG_DIR" ]; then
    echo "Usage: ./log_rotate.sh <log_directory>"
    exit 1
fi

if [ ! -d "$LOG_DIR" ]; then
    echo "Error: Directory does not exist."
    exit 1
fi

# Compress .log files older than 7 days
COMPRESSED=$(find "$LOG_DIR" -name "*.log" -mtime +7 -type f | wc -l)
find "$LOG_DIR" -name "*.log" -mtime +7 -type f -exec gzip {} \;

# Delete .gz files older than 30 days
DELETED=$(find "$LOG_DIR" -name "*.gz" -mtime +30 -type f | wc -l)
find "$LOG_DIR" -name "*.gz" -mtime +30 -type f -delete

echo "Compressed files: $COMPRESSED"
echo "Deleted files: $DELETED"
````

### Sample Output

```
Compressed files: 4
Deleted files: 2
```

---

# 🔹 Task 2: Server Backup Script

## File: backup.sh

```bash
#!/bin/bash
set -euo pipefail

SOURCE="${1:-}"
DEST="${2:-}"

if [ -z "$SOURCE" ] || [ -z "$DEST" ]; then
    echo "Usage: ./backup.sh <source_directory> <backup_destination>"
    exit 1
fi

if [ ! -d "$SOURCE" ]; then
    echo "Error: Source directory does not exist."
    exit 1
fi

mkdir -p "$DEST"

TIMESTAMP=$(date +%Y-%m-%d)
ARCHIVE="$DEST/backup-$TIMESTAMP.tar.gz"

tar -czf "$ARCHIVE" "$SOURCE"

if [ -f "$ARCHIVE" ]; then
    SIZE=$(du -h "$ARCHIVE" | cut -f1)
    echo "Backup created: $ARCHIVE"
    echo "Size: $SIZE"
else
    echo "Backup failed."
    exit 1
fi

# Delete backups older than 14 days
find "$DEST" -name "backup-*.tar.gz" -mtime +14 -type f -delete
```

### Sample Output

```
Backup created: /backups/backup-2026-02-19.tar.gz
Size: 120M
```

---

# 🔹 Task 3: Crontab

## Check current cron jobs

```bash
crontab -l
```

---

## Cron Syntax

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week (0-7)
│ │ │ └──── Month (1-12)
│ │ └────── Day of month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

---

## Cron Entries

### Run log_rotate.sh daily at 2 AM

```
0 2 * * * /path/to/log_rotate.sh /var/log/myapp
```

### Run backup.sh every Sunday at 3 AM

```
0 3 * * 0 /path/to/backup.sh /var/www /backups
```

### Run health check every 5 minutes

```
*/5 * * * * /path/to/health_check.sh
```

---

# 🔹 Task 4: Scheduled Maintenance Script

## File: maintenance.sh

```bash
#!/bin/bash
set -euo pipefail

LOG_FILE="/var/log/maintenance.log"

log() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" >> "$LOG_FILE"
}

log "Maintenance started"

./log_rotate.sh /var/log/myapp >> "$LOG_FILE" 2>&1
log "Log rotation completed"

./backup.sh /var/www /backups >> "$LOG_FILE" 2>&1
log "Backup completed"

log "Maintenance finished"
```

---

## Cron Entry for Maintenance Script (Daily at 1 AM)

```
0 1 * * * /path/to/maintenance.sh
```

