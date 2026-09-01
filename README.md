# Router Control Hub — Dashboard

A beautiful dark-mode dashboard for controlling a ZTE 4G router's network mode (4G LTE / 3G / 2G / Auto) through the router's web API.

## What it does

- **Network mode switching**: Toggle between Auto, 4G LTE, 3G, and 2G bands
- **Real-time speed monitoring**: Live download/upload throughput with animated bars
- **Usage tracking**: Daily, weekly, monthly, and yearly data usage (persisted locally)
- **Status monitoring**: RSRP, SINR, signal bars, APN, connection status

## Architecture

```
[Browser] → [GitHub Pages] → [Cloudflare Tunnel] → [Laptop:8090] → [Router 192.168.0.1]
```

The dashboard frontend is hosted on GitHub Pages (always available). When your laptop
is on, a Cloudflare Tunnel proxies API requests to the laptop, which talks to the
router at `192.168.0.1`.

## Files

| File | Description |
|------|-------------|
| `index.html` | The dashboard frontend (static HTML/CSS/JS) |
| `config.json` | Contains the current Cloudflare Tunnel URL (auto-updated) |
| `router_ctl.py` | The backend server (runs on your laptop) |
| `start-router-hub.sh` | Starts the dashboard + tunnel |
| `update-tunnel-url.sh` | Updates config.json when the tunnel URL changes |

## Setup

1. The backend (`router_ctl.py`) runs on your laptop and must stay on for the
   dashboard to work.
2. A Cloudflare Tunnel exposes the laptop to the internet.
3. The frontend is deployed to GitHub Pages and reads `config.json` for the
   tunnel URL.
