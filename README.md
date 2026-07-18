# portal_gun
Green Portal
2026-07-18 Green Portal Edition — A security-hardened, self-hosted VLESS proxy panel built for Cloudflare Workers.

What Changed From Zeus
Security First: Removed all auto-update and external GitHub fetch vectors. No more silent code injection risks.
Hardened Auth: Salted SHA-256 passwords, 8-character minimum, improved rate limiting (5 attempts / 30 min).
Zero External Dependency: Removed GitHub IP rotation, proxy VIP lists, global message polling, and donation workers.
Complete Rebrand: No traces of the old name. New identity, new colors, new feel.
Premium UI: Dark green neon theme (#0a2f1f, #00ff9d) with a Rick and Morty inspired portal vortex.
Prerequisites
A Cloudflare account (free tier works).
A D1 database created in your Cloudflare dashboard.
(Optional) A Cloudflare API token for the password recovery feature or GraphQL usage stats.
Deployment1. Create a D1 Database
Go to Workers & Pages > D1 in the Cloudflare dashboard and create a new database (e.g., green-portal-db).

Create a Worker
Go to Workers & Pages > Create application > Create Worker. Give it a name (e.g., green-portal).

Bind the Database
In the Worker settings, go to Settings > Variables > Bindings and add a D1 Database binding:

Variable name: DB
Database: select your D1 database
Upload the Code
Replace the default worker code with the contents of _worker.js provided above. Click Save and Deploy.

First Login
Visit https://your-worker.your-subdomain.workers.dev/panel. You will be prompted to set an admin password.

Environment Variables (Optional)
For Cloudflare usage stats to appear in the dashboard, add these Secrets (not plain variables, for security):

Secret Name	Description
CF_API_TOKEN	Cloudflare API token with Account read
CF_ACCOUNT_ID	Your Cloudflare Account ID
These are not required for core proxy functionality. They are only used to show request statistics.

Features- VLESS / WebSocket proxy protocol support
Per-user limits: Volume (GB), Request count, Time expiry, Device/IP limits
Fragment support for improved compatibility
Fingerprint spoofing (Chrome, Firefox, Safari, iOS, Android, etc.)
Content filtering: Block ads and/or adult content per-user
SOCKS5 / HTTP upstream proxy per user
Bulk operations: Activate, deactivate, reset limits, delete
Backup & Restore: Full JSON export/import- Status page: Users can view their own usage at /status/{username}
Auto-reset cycles: Automatic volume/request reset intervals
Iran-Specific Tips
SNI & Host: Use a clean domain (e.g., speedtest.net or your own CDN domain) as the SNI value in your client config.
Fragment: Enable fragment (default 200-3000,1-2) for unstable networks. This is set per-user in the panel.
Clean IPs: Paste known clean IPs (one per line) in the user's IP list. The subscription generator will rotate through them.
Ports: Use standard TLS ports (443, 2053, 2083, 2087, 2096, 8443) for best compatibility with Iranian DPI.
DNS: Ad-blocking DNS (1.1.1.3, AdGuard Family) can be enabled per-user to block government propaganda and tracker domains.
No external fetches: This edition does not phone home to GitHub or any third-party server, making it safer in restricted networks.
Security Best Practices
Use a strong password (12+ characters) for the admin panel.
Do not share your /panel URL publicly. Protect it with Cloudflare Access or keep the subdomain secret.
Storage: The panel stores only metadata (usernames, limits, UUIDs). It does not store traffic content.
Recovery token: Keep a Cloudflare API token safely offline in case you forget the admin password.
HTTPS only: Always access the panel over https://. Cloudflare Workers enforce this by default.
Rotate users periodically: Use the auto-reset feature to Rotate user limits automatically.
Local backups: Use the Export Backup button in Settings regularly.
File Structure
green-portal/
└── _worker.js # Complete single-file Cloudflare Worker
Deploy _worker.js directly. No build step required.

License
This is a derivative work released for security research and personal use. Use responsibly and in accordance with local laws.
