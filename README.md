# 🌐 VPS Domain Management (Nginx + Cloudflare)

A clean and modular guide for hosting applications on a VPS using **Nginx Reverse Proxy** and **Cloudflare DNS + Zero Trust**.

This repository includes ready-to-use templates and best practices for secure and maintainable domain management.

---

## 🚀 Features
- 🟧 Cloudflare-proxied subdomain routing  
- 🔁 Nginx Reverse Proxy configuration templates  
- 🔒 Cloudflare Zero Trust protection for admin panels  
- 📦 Modular templates and folder structure  
- 🌍 Supports multiple apps/domains on the same VPS  

---

## 🏗️ Architecture

| Component | Purpose |
|----------|---------|
| **VPS (Ubuntu)** | Host applications and reverse proxies |
| **Nginx** | Reverse proxy + routing |
| **Cloudflare** | DNS, SSL, security |
| **Zero Trust** | Access control for admin panels |

---

# 📥 Installation

## 1) Install Nginx

```bash
sudo apt update && sudo apt install nginx -y
```

---

# ⚙️ Configure a Domain / Subdomain

## 2) Create Reverse Proxy Config

### 1. Copy template
```bash
sudo cp nginx/templates/reverse-proxy.conf /etc/nginx/sites-available/my-app.com
```

### 2. Edit config
```bash
sudo nano /etc/nginx/sites-available/my-app.com
```

Modify:

- `server_name` → your domain  
- `proxy_pass` → your app port (e.g., http://localhost:3000)

### 3. Enable the site
```bash
sudo ln -s /etc/nginx/sites-available/my-app.com /etc/nginx/sites-enabled/
```

### 4. Test & restart Nginx
```bash
sudo nginx -t
sudo systemctl restart nginx
```

---

# 🌩️ Cloudflare DNS Setup

Go to **Cloudflare → DNS** and add:

| Type | Name | IPv4 Address | Proxy |
|------|------|--------------|--------|
| A | subdomain | YOUR_VPS_IP | Proxied (orange) |

> **SSL/TLS Mode:** `Flexible`

---

# 🛡️ Cloudflare Zero Trust Protection

Secure access to sensitive dashboards (Portainer, Swagger, Grafana, pgAdmin, etc.).

### Steps:
1. Cloudflare Zero Trust → **Access → Applications**
2. Click **Add Application → Self-hosted**
3. Enter domain or subdomain
4. Create a policy:
   - **Action:** Allow  
   - **Include:** Email → *your email*

Only authenticated users (OTP login) can access the panel.
```
