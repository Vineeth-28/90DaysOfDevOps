🐧 Linux Architecture, Processes & systemd – Notes
1️⃣ Core Components of Linux
🔹 Kernel

The core of the OS

Talks directly to hardware (CPU, memory, disk, network)

Responsibilities:

Process management

Memory management

Device drivers

File systems

Runs in kernel space (high privilege)

🔹 User Space

Where users and applications run

Includes:

Shell (bash, zsh)

System utilities (ls, ps, top)

Applications (nginx, docker, java)

Runs in user space (limited privilege)

🔹 Init System (systemd)

The first process started by the kernel (PID 1)

Responsible for:

Starting services

Managing system boot

Restarting failed services

Logging and dependencies

2️⃣ How Processes Are Created & Managed
🔹 Process Creation

A new process is created using:

fork() → creates a copy of the process

exec() → replaces process with a new program

Every process has:

PID (Process ID)

PPID (Parent Process ID)

🔹 Process Lifecycle

Process is created

Gets CPU time from scheduler

May wait for I/O

Completes or gets terminated

3️⃣ Process States (Very Important)
State	Meaning
Running (R)	Currently executing on CPU
Sleeping (S)	Waiting for I/O or event
Uninterruptible Sleep (D)	Waiting for disk/network (cannot be killed easily)
Stopped (T)	Paused (usually by signal)
Zombie (Z)	Process finished but parent hasn’t cleaned it up

➡️ Zombies mean bad parent process behavior

4️⃣ What systemd Does & Why It Matters
🔹 What systemd Is

Modern init and service manager

Replaced older SysV init

Manages services using unit files

🔹 Why systemd Is Important

Automatically restarts crashed services

Manages service dependencies

Centralized logging with journalctl

Essential for production reliability

🔹 Example

If nginx crashes:

systemd can restart it automatically

Logs are available instantly

5️⃣ 5 Linux Commands I Will Use Daily

ps aux → View running processes

top / htop → Real-time CPU & memory usage

systemctl status <service> → Check service health

journalctl -u <service> → View service logs

kill / kill -9 → Stop misbehaving processes

6️⃣ Why This Matters for DevOps

Every container runs on Linux

Kubernetes nodes run Linux

CI/CD runners run Linux

Most production outages involve:

High CPU

Memory leaks

Crashed services

Understanding Linux internals = faster incident resolution

✍️ End of Notes