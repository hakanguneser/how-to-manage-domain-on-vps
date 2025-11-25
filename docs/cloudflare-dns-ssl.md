# ☁️ Cloudflare DNS & SSL Setup

## 1. DNS Records
Go to the **DNS** section in your Cloudflare dashboard and add an A Record for your application.

| Type | Name | Content (IPv4) | Proxy Status |
| :--- | :--- | :--- | :--- |
| **A** | `app` | `<YOUR_VPS_IP_ADDRESS>` | ✅ Proxied |
| **A** | `@` | `<YOUR_VPS_IP_ADDRESS>` | ✅ Proxied |

> **⚠️ Note on Subdomains:** Cloudflare Free Plan does not support multi-level subdomains (e.g., `api.dev.example.com`). 
> **Solution:** Flatten your structure using hyphens (e.g., `api-dev.example.com`).

## 2. SSL/TLS Settings
To avoid "Redirect Loops" or "522 Errors", ensure your SSL settings are correct.

1.  Go to **SSL/TLS** menu.
2.  Set encryption mode to **Flexible**.
    * *Reason:* Cloudflare talks to your VPS via HTTP (Port 80), but visitors talk to Cloudflare via HTTPS.
3.  Go to **Edge Certificates** tab.
    * Ensure "Always Use HTTPS" is **OFF** initially (Turn ON after testing).
    * Wait for the certificate status to become **"Active"**.