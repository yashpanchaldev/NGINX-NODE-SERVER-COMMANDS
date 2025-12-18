# NGINX-NODE-SERVER-COMMANDS

# 🚀 Node.js Production Deployment Notes (AWS EC2)

This repository contains **complete production-level notes and commands** for deploying, testing, monitoring, and maintaining a **Node.js backend application** on **AWS EC2** using **NGINX, PM2, and MySQL**.

---

## 🧱 Tech Stack
- **Server:** AWS EC2 (Ubuntu)
- **Backend:** Node.js
- **Process Manager:** PM2
- **Reverse Proxy:** NGINX
- **Database:** MySQL
- **Access:** SSH (Terminal / Bitvise)

---

## 📐 Architecture
**User** -> **NGINX** -> **Node.js App (PM2)** -> **MySQL**

---

## 🔹 NGINX Management

### Basic Controls
| Action | Command |
| :--- | :--- |
| **Start** | `sudo systemctl start nginx` |
| **Stop** | `sudo systemctl stop nginx` |
| **Restart** | `sudo systemctl restart nginx` |
| **Reload** | `sudo systemctl reload nginx` |
| **Status** | `sudo systemctl status nginx` |
| **Test Config** | `sudo nginx -t` |

### 📊 Logs & Monitoring
- **Access Logs:** `sudo tail -f /var/log/nginx/access.log`
- **Error Logs:** `sudo tail -f /var/log/nginx/error.log`

### 🔎 API Filtering
- **API Only:** `sudo tail -f /var/log/nginx/access.log | grep "/api"`
- **POST Only:** `sudo tail -f /var/log/nginx/access.log | grep "POST"`
- **Live Status Codes:** `sudo tail -f /var/log/nginx/access.log | awk '{print $9}'`

---

## ⚙️ PM2 (Process Manager)

- **Start App:** `pm2 start app.js --name app`
- **Restart:** `pm2 restart app`
- **Stop:** `pm2 stop app`
- **List All:** `pm2 list`
- **Live Logs:** `pm2 logs`
- **Save for Reboot:** `pm2 startup` && `pm2 save`

---

## 🧪 Testing & Network

### Port Check
- `sudo ss -tulpn | grep 8000`

### API Testing (CURL)
- **Local:** `curl http://localhost:8000/api/health`
- **Public:** `curl http://<EC2_PUBLIC_IP>/api/health`

---

## 🔥 Firewall (UFW)
- **Status:** `sudo ufw status`
- **Allow NGINX:** `sudo ufw allow 'Nginx Full'`
- **Allow SSH:** `sudo ufw allow OpenSSH`

---

## 🛢 MySQL Management
- **Status:** `sudo systemctl status mysql`
- **Restart:** `sudo systemctl restart mysql`
- **Logs:** `sudo tail -f /var/log/mysql/error.log`

---

## 🩺 Server Health Check
```bash
sudo systemctl status nginx
pm2 list
sudo systemctl status mysql
df -h  # Disk Space
free -h # Memory
