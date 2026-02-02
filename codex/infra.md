# Infrastructure Setup

## Overview

```
User → watanabefishing.site → Cloudflare → Tunnel → Bastion → Dev Box:8080
```

## Domain: watanabefishing.site

**Registrar:** Namecheap
**Purchased:** Feb 2, 2026
**Expires:** Feb 2, 2027 (auto-renew on)

---

## Namecheap Configuration

### Nameservers (DONE ✅)

Changed from Namecheap BasicDNS to Custom DNS:

```
miki.ns.cloudflare.com
yichun.ns.cloudflare.com
```

This delegates all DNS to Cloudflare.

---

## Cloudflare Configuration

### Domain Status
- **Added to Cloudflare:** Yes
- **Plan:** Free
- **Status:** Pending (waiting for nameserver propagation)

### DNS Records (PENDING - needs validation)

**To Add:**
| Type  | Name | Target | Proxy |
|-------|------|--------|-------|
| CNAME | @    | e1981539-b6a3-47b9-b0c9-7045460830b1.cfargotunnel.com | Proxied |

**To Delete (after CNAME works):**
| Type  | Name | Content | Notes |
|-------|------|---------|-------|
| A     | @    | 162.255.119.201 | Namecheap parking page |
| CNAME | www  | parkingpage... | Namecheap parking page |

### Cloudflare Tunnel

**Tunnel Name:** dmz-tunnel
**Tunnel ID:** e1981539-b6a3-47b9-b0c9-7045460830b1
**Status:** HEALTHY
**Type:** Locally configured (config file on bastion)

The tunnel is already running and used by nagahama-group.com.

---

## Bastion Configuration (TODO)

The bastion box runs `cloudflared` with a local config file.

### Config File Location
Likely at: `/etc/cloudflared/config.yml` or `~/.cloudflared/config.yml`

### Add Hostname
Need to add watanabefishing.site to the ingress rules:

```yaml
ingress:
  # ... existing rules ...

  - hostname: watanabefishing.site
    service: http://dev-box-ip:8080

  # Catch-all (must be last)
  - service: http_status:404
```

Then restart cloudflared:
```bash
sudo systemctl restart cloudflared
```

---

## Dev Box Configuration

### Docker Setup
The site runs via Docker with nginx serving static files.

**Port:** 8080
**Container:** nginx:stable-alpine (via docker-compose)

### Running the Site
```bash
cd /path/to/watanabe-fishing
docker-compose up -d
```

### Checking Status
```bash
docker-compose ps
docker-compose logs web
```

---

## Architecture Diagram

```
┌────────────────────────────────────────────────────────────────┐
│                        INTERNET                                 │
└────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌────────────────────────────────────────────────────────────────┐
│                    NAMECHEAP (Registrar)                       │
│                                                                 │
│  watanabefishing.site                                          │
│  NS → miki.ns.cloudflare.com                                   │
│  NS → yichun.ns.cloudflare.com                                 │
└────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌────────────────────────────────────────────────────────────────┐
│                      CLOUDFLARE                                 │
│                                                                 │
│  DNS:  @ CNAME → tunnel-id.cfargotunnel.com                    │
│  SSL:  Full (automatic)                                        │
│  CDN:  Proxied (orange cloud)                                  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │              Cloudflare Tunnel (dmz-tunnel)              │   │
│  │                                                          │   │
│  │  Encrypted tunnel, no public IP needed                   │   │
│  └─────────────────────────────────────────────────────────┘   │
└────────────────────────────────────────────────────────────────┘
                              │
                              │ (encrypted tunnel)
                              ▼
┌────────────────────────────────────────────────────────────────┐
│                     BASTION BOX                                 │
│                                                                 │
│  Running: cloudflared daemon                                    │
│  Config:  /etc/cloudflared/config.yml (local)                  │
│                                                                 │
│  Ingress rule:                                                 │
│    watanabefishing.site → http://dev-box:8080                  │
└────────────────────────────────────────────────────────────────┘
                              │
                              │ (internal network)
                              ▼
┌────────────────────────────────────────────────────────────────┐
│                       DEV BOX                                   │
│                                                                 │
│  Docker: watanabe-fishing container                            │
│  Port:   8080 → nginx:80                                       │
│  Serves: /usr/share/nginx/html (static files)                  │
└────────────────────────────────────────────────────────────────┘
```

---

## Checklist

### Done
- [x] Domain purchased (Namecheap)
- [x] Nameservers changed to Cloudflare
- [x] Domain added to Cloudflare
- [x] Project scaffolding created

### Pending (needs validation)
- [ ] CNAME record saved in Cloudflare
- [ ] Delete parking page DNS records
- [ ] Nameserver propagation complete

### Todo (after validation)
- [ ] Add hostname to cloudflared config on bastion
- [ ] Restart cloudflared service
- [ ] Test site loads via domain
- [ ] Build actual landing page

---

## Existing Sites (for reference)

These use the same infrastructure pattern:

| Domain | Tunnel | Status |
|--------|--------|--------|
| nagahama-group.com | dmz-tunnel | Working |
| bettahbus.com | (unknown) | Working |

---

## Troubleshooting

### Site not loading after setup

1. **Check nameserver propagation:**
   ```bash
   dig watanabefishing.site NS
   ```
   Should show Cloudflare nameservers.

2. **Check Cloudflare status:**
   Dashboard should show "Active" not "Pending"

3. **Check tunnel status:**
   Zero Trust → Networks → Connectors
   Should show "HEALTHY"

4. **Check cloudflared config:**
   ```bash
   cat /etc/cloudflared/config.yml
   ```
   Verify hostname is in ingress rules.

5. **Check Docker:**
   ```bash
   docker-compose ps
   curl localhost:8080
   ```
   Should return HTML.

### SSL errors

Cloudflare handles SSL automatically. If issues:
- SSL/TLS → Overview → Set to "Full" or "Full (strict)"
- Wait 15 minutes for certificate provisioning
