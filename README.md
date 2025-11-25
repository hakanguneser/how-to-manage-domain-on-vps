# 🌐 How to Manage Domains on VPS (Nginx + Cloudflare)

A practical guide and template collection for hosting web applications on a VPS (Ubuntu) using **Nginx** as a Reverse Proxy and **Cloudflare** for DNS & Security.

## 🎯 Goal
To easily connect domains and subdomains to specific ports on a VPS while securing sensitive admin panels (like Portainer, Swagger, Databases) using Cloudflare Zero Trust.

## 🏗️ Architecture
* **Infrastructure:** VPS (Ubuntu 20.04/22.04/24.04)
* **Web Server:** Nginx (Reverse Proxy)
* **DNS & Security:** Cloudflare (Flexible SSL)
* **Access Control:** Cloudflare Zero Trust

---

## 🚀 Quick Start

### 1. Setup Nginx
First, install Nginx on your VPS:
\\\Bash
sudo apt update && sudo apt install nginx -y
\\\

### 2. Create a New Domain Config
Use the provided template to create a new configuration file for your domain/subdomain.

1.  Copy the template:
    \\\bash
    sudo cp nginx/templates/reverse-proxy.conf /etc/nginx/sites-available/my-app.com
    \\\

2.  Edit the file:
    \\\bash
    sudo nano /etc/nginx/sites-available/my-app.com
    \\\
    *Change \server_name\ to your domain and \proxy_pass\ to your app's port.*

3.  Activate the site:
    \\\Bash
    sudo ln -s /etc/nginx/sites-available/my-app.com /etc/nginx/sites-enabled/
    \\\

4.  Test and Restart Nginx:
    \\\Bash
    sudo nginx -t
    sudo systemctl restart nginx
    \\\

### 3. Setup DNS (Cloudflare)
Go to Cloudflare Dashboard -> **DNS** and add an **A Record**:

| Type | Name | Content (IPv4) | Proxy Status |
| :--- | :--- | :--- | :--- |
| **A** | \subdomain\ | \YOUR_VPS_IP\ | ✅ Proxied |

> **⚠️ Important:** Ensure your Cloudflare SSL/TLS mode is set to **Flexible**.

---

## 🛡️ Security: Cloudflare Zero Trust

To protect admin panels (like Portainer or Swagger UI) from public access:

1.  Go to **Cloudflare Zero Trust** -> **Access** -> **Applications**.
2.  Add a **Self-hosted** application.
3.  Enter your **Subdomain** and **Domain**.
4.  Create a **Policy**:
    * **Action:** Allow
    * **Include:** Selector \Email\ -> Value \your-email@example.com\

Now, only you can access the dashboard via email OTP.

---

## 📂 Repository Structure
* \
ginx/templates/\ - Ready-to-use configuration files.
* \docs/\ - Detailed step-by-step guides.

## 🤝 Contributing
Feel free to open a Pull Request to improve the configurations!
