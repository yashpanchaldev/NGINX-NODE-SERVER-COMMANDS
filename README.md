# NGINX-NODE-SERVER-COMMANDS

# 🚀 Node.js Production Deployment Notes (AWS EC2)

This repository contains **complete production-level notes and commands** for deploying, testing, monitoring, and maintaining a **Node.js backend application** on **AWS EC2** using **NGINX, PM2, and MySQL**.

These notes are based on **real production experience** and are useful for:
- Backend developers
- DevOps beginners
- Production debugging
- Interview preparation

---

## 🧱 Tech Stack

- Server: AWS EC2 (Ubuntu)
- Backend: Node.js
- Process Manager: PM2
- Reverse Proxy: NGINX
- Database: MySQL
- Access: SSH (Terminal / Bitvise)

---

## 📐 Architecture
User (Browser / Mobile)
|
v
NGINX
|
v
Node.js App (PM2)
|
v
MySQL


---

## 🔹 NGINX Management

### Start NGINX

sudo systemctl start nginx

Stop NGINX
sudo systemctl stop nginx

Restart NGINX
sudo systemctl restart nginx

Reload NGINX (Zero Downtime)
sudo systemctl reload nginx

Check NGINX Status
sudo systemctl status nginx

🔍 Test NGINX Configuration (Mandatory)
sudo nginx -t


Expected output:

syntax is ok
test is successful

📊 NGINX Logs (Live Monitoring)
Access Logs
sudo tail -f /var/log/nginx/access.log

Error Logs
sudo tail -f /var/log/nginx/error.log

🔎 API Request Filtering
Only API Requests
sudo tail -f /var/log/nginx/access.log | grep "/api"

Only POST Requests
sudo tail -f /var/log/nginx/access.log | grep "POST"

Specific API Endpoint
sudo tail -f /var/log/nginx/access.log | grep "/api/login"

📈 HTTP Status Code Analysis
Count All Status Codes
awk '{print $9}' /var/log/nginx/access.log | sort | uniq -c

Live Status Codes
sudo tail -f /var/log/nginx/access.log | awk '{print $9}'

Show Errors Only (4xx & 5xx)
sudo tail -f /var/log/nginx/access.log | grep -E " 4[0-9]{2} | 5[0-9]{2} "

⚙️ PM2 (Node.js Process Manager)
Start Application
pm2 start app.js --name app

Restart Application
pm2 restart app

Stop Application
pm2 stop app

Delete Application
pm2 delete app

List Applications
pm2 list

📝 PM2 Logs
Live Logs
pm2 logs

Application Logs
pm2 logs app

Error Logs Only
pm2 logs app --err

Clear Logs
pm2 flush

🔁 PM2 Auto Start on Server Reboot
pm2 startup
pm2 save

🌐 Port & Process Testing
Check Listening Port
sudo ss -tulpn | grep 8000

Check Node Process
ps aux | grep node

🧪 API Testing (CURL)
Local Testing
curl http://localhost:8000/api/health

Production Testing
curl http://<EC2_PUBLIC_IP>/api/health

Check Headers
curl -I http://<EC2_PUBLIC_IP>

🔥 Firewall (UFW)
Check Firewall Status
sudo ufw status

Allow NGINX
sudo ufw allow 'Nginx Full'

Allow SSH
sudo ufw allow OpenSSH

Reload Firewall
sudo ufw reload

🛢 MySQL Management
Check MySQL Status
sudo systemctl status mysql

Restart MySQL
sudo systemctl restart mysql

MySQL Error Logs
sudo tail -f /var/log/mysql/error.log

🩺 Full Server Health Check
sudo systemctl status nginx
pm2 list
sudo systemctl status mysql
df -h
free -h

❌ Common Production Issues
API Not Working
pm2 logs
sudo tail -f /var/log/nginx/error.log

502 Bad Gateway
sudo nginx -t
pm2 list

Server Rebooted
pm2 resurrect

⚠️ Important Notes

Never access /var/lib/mysql manually

Always test NGINX config before restart

Prefer reload instead of restart

PM2 keeps the app alive after crashes or reboots

👨‍💻 Author

Yash
Node.js Backend Developer
AWS EC2 | NGINX | PM2 | MySQL
