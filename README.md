# 🌐 Apache Web Server Deployment

A hands-on Linux lab demonstrating how to deploy and configure
an Apache web server on Rocky Linux — running a real service
accessible over the network.

---

## 📌 What is Apache?

Apache (httpd) is one of the most widely used web servers in the world.
It powers millions of websites and is a core skill for any
Linux sysadmin or DevOps engineer.

---

## 🎯 What I Did in This Lab

- ✅ Installed Apache (httpd) on Rocky Linux 9
- ✅ Enabled and started the service with systemctl
- ✅ Configured firewall rules (HTTP port 80 / HTTPS port 443)
- ✅ Deployed a test website
- ✅ Configured a Virtual Host
- ✅ Verified with curl and browser

---

## 🛠️ Tools & Commands Used

| Command | Purpose |
|---|---|
| `dnf install httpd` | Install Apache web server |
| `systemctl enable --now httpd` | Enable and start Apache |
| `firewall-cmd` | Open HTTP/HTTPS ports |
| `apachectl configtest` | Validate Apache configuration |
| `curl http://localhost` | Test server response |
| `tail -f /var/log/httpd/` | Monitor access and error logs |

---

## 💻 Environment

- **OS:** Rocky Linux 9 / RHEL 9
- **Virtualization:** VirtualBox
- **Web Server:** Apache httpd 2.4
- **Firewall:** firewalld

---

## ⚙️ Key Configuration
```bash
# Install Apache
dnf install httpd -y

# Enable on boot and start immediately
systemctl enable --now httpd

# Open firewall ports
firewall-cmd --add-service=http --permanent
firewall-cmd --add-service=https --permanent
firewall-cmd --reload

# Deploy test page
echo "<h1>Apache is Running!</h1>" > /var/www/html/index.html

# Check Apache is listening
ss -tlnp | grep :80
```

---

## 🌍 Virtual Host Configuration
```bash
# /etc/httpd/conf.d/mysite.conf
<VirtualHost *:80>
    ServerName mysite.local
    DocumentRoot /var/www/mysite
    ErrorLog /var/log/httpd/mysite_error.log
    CustomLog /var/log/httpd/mysite_access.log combined
</VirtualHost>
```

---

## ✅ Verification Output
```
$ systemctl status httpd
● httpd.service - The Apache HTTP Server
     Active: active (running)

$ curl -I http://localhost
HTTP/1.1 200 OK
Server: Apache/2.4.57 (Rocky Linux)
---
## 📋 Skills Demonstrated

- Web server installation and management
- systemctl service control
- Firewall configuration with firewalld
- Virtual host setup
- Apache log monitoring
- Static website deployment
---
## 👤 Author

**Hubaib** — Desktop Engineer | Linux Enthusiast
📍 IIM Kozhikode
🔗 [GitHub Profile](https://github.com/kphubaib)
