# 🛡️ Securing Apps with Cloudflare Zero Trust

If you are hosting internal tools (e.g., Portainer, Admin Dashboards, Swagger UI), you should not expose them to the public internet. Use Zero Trust to add an authentication layer.

## Setup Steps

1.  **Open Zero Trust Dashboard:**
    * Go to Cloudflare Dashboard -> Zero Trust.

2.  **Create Application:**
    * Navigate to **Access** -> **Applications** -> **Add an Application**.
    * Select **Self-hosted**.

3.  **Configure Application:**
    * **Application Name:** e.g., "Portainer Admin"
    * **Subdomain:** `portainer`
    * **Domain:** `example.com`
    * *(Optional)* **Path:** `/api/docs/` (To protect specific routes like Swagger).

4.  **Add Policy (Who can access?):**
    * **Policy Name:** "Admin Only"
    * **Action:** Allow
    * **Configure Rules -> Include:**
        * **Selector:** `Email`
        * **Value:** `your-email@example.com`

## Result
When someone visits the URL, they will be redirected to a Cloudflare login page. Only the defined email addresses can receive a login code.