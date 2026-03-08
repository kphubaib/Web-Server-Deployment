# 🌐 Apache Web Server Deployment

**Goal:** Run a real service on Linux — configure and deploy an Apache web server with firewall rules.

---

## Lab Environment

- OS: Rocky Linux 9 / RHEL 9
- Web Server: Apache (httpd)
- Firewall: firewalld

---

## Step-by-Step Deployment

### Step 1 — Install Apache

```bash
# RHEL / Rocky Linux
dnf install httpd -y

# Ubuntu/Debian
apt install apache2 -y
```

---

### Step 2 — Enable and Start Apache

```bash
# Enable on boot + start immediately
systemctl enable --now httpd

# Verify it's running
systemctl status httpd
```

---

### Step 3 — Configure Firewall

```bash
# Allow HTTP (port 80) and HTTPS (port 443)
firewall-cmd --add-service=http --permanent
firewall-cmd --add-service=https --permanent
firewall-cmd --reload

# Verify open services
firewall-cmd --list-services
```

---

### Step 4 — Deploy a Test Website

```bash
# Navigate to Apache web root
cd /var/www/html

# Create a simple test page
cat > index.html << 'EOF'
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Linux Server — Live</title>
    <style>
        body { font-family: monospace; background: #0d1117; color: #58a6ff;
               display: flex; justify-content: center; align-items: center;
               height: 100vh; margin: 0; flex-direction: column; }
        h1   { font-size: 2rem; }
        p    { color: #8b949e; }
    </style>
</head>
<body>
    <h1>🐧 Apache Server is Running</h1>
    <p>Deployed on Rocky Linux 9 | Configured by Hubaib</p>
</body>
</html>
EOF
```

---

### Step 5 — Configure a Virtual Host (Optional but Impressive)

```bash
# Create a virtual host config
cat > /etc/httpd/conf.d/mysite.conf << 'EOF'
<VirtualHost *:80>
    ServerName mysite.local
    DocumentRoot /var/www/mysite
    ErrorLog /var/log/httpd/mysite_error.log
    CustomLog /var/log/httpd/mysite_access.log combined

    <Directory /var/www/mysite>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
EOF

# Create site directory
mkdir -p /var/www/mysite

# Test Apache config syntax
apachectl configtest

# Reload Apache
systemctl reload httpd
```

---

### Step 6 — Verify

```bash
# From the server itself
curl http://localhost

# Check Apache is listening
ss -tlnp | grep :80

# View logs
tail -f /var/log/httpd/access_log
tail -f /var/log/httpd/error_log
```

---

## Verification Output

```
$ systemctl status httpd
● httpd.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled)
     Active: active (running) since ...

$ curl -I http://localhost
HTTP/1.1 200 OK
Server: Apache/2.4.57 (Rocky Linux)
```

---

## Skills Demonstrated

- Package installation and service management with `systemctl`
- Firewall configuration with `firewalld`
- Apache virtual host configuration
- Web server log analysis
- Static web content deployment

---

## Resume Line

> *Deployed Apache web server on Rocky Linux, configured firewall rules with firewalld, and hosted a static website with virtual host configuration.*
