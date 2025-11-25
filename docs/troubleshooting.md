# 🔧 Troubleshooting Common Errors

### 🔴 Host Error (521 / 522)
**Cause:** Cloudflare cannot connect to your VPS.
**Fixes:**
* Check if Nginx is running: `sudo systemctl status nginx`
* Check Firewall (UFW): Ensure Port 80 is open.
    ```bash
    sudo ufw allow 'Nginx Full'
    ```

### 🔴 502 Bad Gateway
**Cause:** Nginx is running, but the backend application (Java, Node, Python) is down.
**Fixes:**
* Check if your app is running on the specific port:
    ```bash
    curl -I [http://127.0.0.1](http://127.0.0.1):YOUR_PORT
    ```
* If using Docker, ensure the container is running: `docker ps`

### 🔴 SSL Cipher Mismatch / Protocol Error
**Cause:** Cloudflare SSL certificate is not ready yet or you are using a deep subdomain.
**Fixes:**
* Wait 15-30 mins for the certificate to activate.
* Ensure you are not using 4th level domains (e.g., `a.b.domain.com` ❌ -> `a-b.domain.com` ✅).

### 🔴 Google "Deceptive Site Ahead"
**Cause:** New domain presenting a login screen (like Portainer) triggers Google's phishing detectors.
**Fixes:**
* Implement **Cloudflare Zero Trust** (so Google bots can't see the login form).
* Submit a report to [Google Safe Browsing](https://safebrowsing.google.com/safebrowsing/report_error/).