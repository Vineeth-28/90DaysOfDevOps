


## 🔹 Part 1: Launch Cloud Instance & SSH

### 1️⃣ Create Instance

* Cloud: **AWS EC2 (Ubuntu 22.04)** or **Utho**
* Instance type: `t2.micro` (AWS Free Tier)
* Key pair: download `.pem`
* Security Group:

  * SSH → port `22`
  * HTTP → port `80` (IMPORTANT)

---

### 2️⃣ Connect via SSH

```bash
chmod 400 your-key.pem
ssh -i your-key.pem ubuntu@<INSTANCE_PUBLIC_IP>
```

📸 **Screenshot:** terminal showing successful SSH login
(save as `ssh-connection.png`)

---

## 🔹 Part 2: Install Docker & Nginx

### 3️⃣ Update system

```bash
sudo apt update && sudo apt upgrade -y
```

---

### 4️⃣ Install Docker

```bash
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
docker --version
```

📸 Screenshot docker version (`docker-nginx.png`)

---

### 5️⃣ Install Nginx

```bash
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

Verify:

```bash
systemctl status nginx
```

---

## 🔹 Part 3: Verify Web Access

Open browser:

```
http://<INSTANCE_PUBLIC_IP>
```

✅ You should see **“Welcome to nginx!”**

📸 Screenshot this page
(save as `nginx-webpage.png`)

---

## 🔹 Part 4: Extract Nginx Logs

### 6️⃣ View logs

```bash
sudo cat /var/log/nginx/access.log
sudo cat /var/log/nginx/error.log
```

---

### 7️⃣ Save logs to file

```bash
sudo cat /var/log/nginx/access.log > nginx-logs.txt
```

Move to home:

```bash
sudo chown ubuntu:ubuntu nginx-logs.txt
```

---

### 8️⃣ Download logs to local machine

On **your local system**:

```bash
scp -i your-key.pem ubuntu@<INSTANCE_PUBLIC_IP>:~/nginx-logs.txt .
```

✅ File downloaded successfully


# 🌐 Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

## 🔧 Commands Used
- ssh -i key.pem ubuntu@<ip>
- sudo apt update && sudo apt upgrade -y
- sudo apt install docker.io -y
- sudo systemctl start docker
- sudo apt install nginx -y
- sudo systemctl start nginx
- systemctl status nginx
- cat /var/log/nginx/access.log
- scp nginx-logs.txt to local machine

---

## ⚠️ Challenges Faced
- Initially could not access Nginx webpage
- Resolved by allowing port 80 in the security group
- Learned importance of cloud firewall rules

---

## 📘 What I Learned
- How to launch and access a cloud VM using SSH
- Installing and managing services using systemctl
- How security groups control inbound traffic
- Where Nginx logs are stored and how to extract them
- Basic cloud server troubleshooting steps

---

## ✅ Verification
- SSH connection successful
- Nginx webpage accessible via browser
- Logs extracted and downloaded successfully

✍️ *End of Day 08*
```

---

# 📂 Files you should commit

Inside `2026/day-08/`:

```
day-08-cloud-deployment.md
nginx-logs.txt
ssh-connection.png
nginx-webpage.png
docker-nginx.png
```

---

