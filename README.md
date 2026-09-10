# RSV Server - Deploy Guide (Step by Step)

## Step 1: Connect to Server

```bash
ssh -p 2222 kyserver@100.125.40.42
```

---

## Step 2: Deploy Your Project

```bash
deploy <project-name> <git-repo-url> <domain> [port]
```

**Example:**
```bash
deploy my-app https://github.com/myorg/my-app.git app.rvstechsolution.com 8080
```

Wait for it to finish (usually 2-5 minutes).

---

## Step 3: Add Cloudflare Tunnel

1. Open browser → https://one.dash.cloudflare.com
2. Go to **Networks** → **Tunnels**
3. Click **Configure** on the tunnel
4. Go to **Public Hostnames** tab
5. Click **Add a public hostname**
6. Fill in:
   - **Hostname:** `your-domain.com`
   - **Service Type:** `HTTP`
   - **URL:** `localhost:PORT`
7. Click **Save**

---

## Step 4: Test

Open browser and go to:
```
https://your-domain.com
```

---

## Common Commands

| What | Command |
|------|---------|
| See running containers | `docker ps` |
| See my project containers | `docker ps --filter name=PROJECT` |
| View logs | `docker logs CONTAINER -f` |
| Restart project | `cd /var/www/PROJECT && docker compose -f docker-compose.prod.yml restart` |
| Stop project | `cd /var/www/PROJECT && docker compose -f docker-compose.prod.yml down` |
| Update project | `cd /var/www/PROJECT && git pull && docker compose -f docker-compose.prod.yml up -d --build` |

---

## Currently Running

| App | URL |
|-----|-----|
| Portainer | https://portainer.rvstechsolution.com |
| Printer | https://printer.rvstechsolution.com |
| Sellsim | https://sellsim.kneayerng.com |

---

## Troubleshooting

**Problem: Container keeps restarting**
```bash
docker logs CONTAINER-NAME
```

**Problem: Port already used**
```bash
sudo lsof -i :PORT
```

**Problem: Can't connect to database**
```bash
docker exec PROJECT_db pg_isready -U USERNAME -d DATABASE
```
