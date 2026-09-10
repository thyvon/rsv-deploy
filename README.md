# RSV Server - Deploy

## One Command Deploy

```bash
deploy <project> <repo-url> <domain> [port]
```

### Examples

```bash
deploy printer-managment https://github.com/rsv/printer-managment.git printer.rvstechsolution.com
deploy my-app https://github.com/org/app.git app.rvstechsolution.com 8081
```

## What It Does

1. Clones repo to `/var/www/<project>`
2. Creates `.env` with random DB password
3. Creates `docker-compose.prod.yml` from template (if missing)
4. Builds and starts all containers
5. Shows you the Cloudflare tunnel config to add

## After Deploy

Add hostname in **Cloudflare** → **Zero Trust** → **Tunnels** → **Public Hostnames**:
- **Hostname**: `<domain>`
- **Service**: `HTTP`  
- **URL**: `localhost:<port>`

## Quick Commands

| Task | Command |
|------|---------|
| Deploy | `deploy <project> <repo> <domain> [port]` |
| Restart | `cd /var/www/<project> && docker compose -f docker-compose.prod.yml restart` |
| Stop | `cd /var/www/<project> && docker compose -f docker-compose.prod.yml down` |
| Logs | `cd /var/www/<project> && docker compose -f docker-compose.prod.yml logs -f` |
| Update | `cd /var/www/<project> && git pull && docker compose -f docker-compose.prod.yml up -d --build` |
| Status | `docker ps` |
