# ROCK STAR / Quotex Premium - License Server

## Features
- ✅ One License Key = One Device only
- ✅ Time limited keys: 10 min, 30 min, 1 hour, 1 day, 1 month, Lifetime
- ✅ Admin panel to generate / revoke / unbind keys
- ✅ Simple JSON storage (no database needed)
- ✅ Easy to deploy on any VPS / Railway / Render / VPS

## Quick Start (Local)

```bash
cd server
npm install
node server.js
```

Server runs on http://localhost:3847

Admin panel: open the same URL in browser  
Default password: `ROCKSTAR@2026`

## Deploy on VPS (Ubuntu)

```bash
# Install node if needed
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# Upload the server folder, then:
cd server
npm install
# Change password:
export ADMIN_PASSWORD="YourStrongPasswordHere"
# Run with PM2 (recommended)
npm install -g pm2
pm2 start server.js --name license-server
pm2 save
pm2 startup
```

Or use Railway / Render / Fly.io – just set root to `server` folder.

## After Deploy – Update Extension

1. Open file `ewpntwciqyxepolqqvct.js`
2. Change this line:

```js
const LICENSE_SERVER = "https://YOUR-SERVER-DOMAIN.com";
```

to your real server URL, example:

```js
const LICENSE_SERVER = "https://license.yourdomain.com";
// or
const LICENSE_SERVER = "http://123.45.67.89:3847";
```

3. Re-zip the whole "Quotex Premium" folder and load the extension again (or distribute the new zip).

## How to give licenses

1. Open admin panel → login with password
2. Select duration (10m / 30m / 1h / 1d / 1month / lifetime)
3. Click Generate
4. Copy the key (format: ROCK-XXXX-XXXX-XXXX) and give to customer

## Device Binding

- First time a key is used → it gets locked to that browser/device
- Same key on another PC/browser → Access Denied
- Admin can click "Unbind" to free the key for a new device

## API Summary

| Endpoint | Method | Auth | Description |
|----------|--------|------|-------------|
| /api/validate | POST | - | {key, fingerprint} → validate & bind |
| /api/heartbeat | POST | - | keep-alive |
| /api/admin/generate | POST | Admin | create new keys |
| /api/admin/revoke | POST | Admin | revoke key |
| /api/admin/unbind | POST | Admin | free device |
| /api/admin/list | GET | Admin | list all keys |
| /api/admin/stats | GET | Admin | counts |

