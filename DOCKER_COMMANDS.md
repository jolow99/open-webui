# Docker Commands Reference for Open WebUI

This document contains all the essential Docker commands for building, running, and managing your Open WebUI container.

## 🔨 Building the Container

```bash
# Build the Docker image with your custom tag
docker build -t publicai-openwebui .
```

## 🚀 Running the Container

```bash
# Run the container (basic command)
docker run -d -p 3000:8080 --name publicai-openwebui publicai-openwebui
```

## 🛠️ Management Commands

### Stop and Remove Container
```bash
# Stop the running container
docker stop publicai-openwebui

# Remove the container (to rebuild/restart fresh)
docker rm publicai-openwebui
```

### Full Rebuild Workflow
```bash
# Complete rebuild and restart sequence
docker stop publicai-openwebui
docker rm publicai-openwebui
docker build -t publicai-openwebui .
docker run -d -p 3000:8080 --name publicai-openwebui publicai-openwebui
```

## 📊 Monitoring Commands

```bash
# Check running containers
docker ps

# View container logs
docker logs publicai-openwebui

# View live logs (follow)
docker logs -f publicai-openwebui

# Check last 20 log lines
docker logs publicai-openwebui --tail 20
```

## 🔧 Enhanced Run Command (Recommended)

For production use, consider this enhanced version with persistent data:

```bash
# Run with persistent data volume
docker run -d \
  -p 3000:8080 \
  -v open-webui-data:/app/backend/data \
  --name publicai-openwebui \
  --restart unless-stopped \
  publicai-openwebui
```

This version:
- Creates a persistent volume for your data
- Automatically restarts the container if it stops
- Maps to port 3000 on your host machine

## 📝 Quick Reference

| Action | Command |
|--------|---------|
| **Build** | `docker build -t publicai-openwebui .` |
| **Run** | `docker run -d -p 3000:8080 --name publicai-openwebui publicai-openwebui` |
| **Stop** | `docker stop publicai-openwebui` |
| **Remove** | `docker rm publicai-openwebui` |
| **Logs** | `docker logs publicai-openwebui` |
| **Access** | **http://localhost:3000** |

## 💡 Pro Tips

1. **Always rebuild after code changes**: Any modifications to the source code require a rebuild
2. **Use consistent naming**: Stick with `publicai-openwebui` for both image and container names
3. **Check logs first**: If something doesn't work, always check `docker logs` first
4. **Port consistency**: Remember it's always `host_port:8080` (container serves on 8080 internally)

## 🔄 Common Workflows

### Development Workflow
When making changes to the code:
```bash
# Stop current container
docker stop publicai-openwebui

# Remove container
docker rm publicai-openwebui

# Rebuild with changes
docker build -t publicai-openwebui .

# Run updated container
docker run -d -p 3000:8080 --name publicai-openwebui publicai-openwebui

# Check it's working
curl -s -o /dev/null -w "%{http_code}" http://localhost:3000
```

### Troubleshooting Workflow
When something isn't working:
```bash
# Check if container is running
docker ps

# Check container health
docker ps -a

# View recent logs
docker logs publicai-openwebui --tail 50

# View live logs for debugging
docker logs -f publicai-openwebui
```

### Clean Reset Workflow
For a completely fresh start:
```bash
# Stop and remove container
docker stop publicai-openwebui
docker rm publicai-openwebui

# Remove the image (optional - forces complete rebuild)
docker rmi publicai-openwebui

# Remove persistent data (optional - loses all data)
docker volume rm open-webui-data

# Rebuild and run fresh
docker build -t publicai-openwebui .
docker run -d -p 3000:8080 --name publicai-openwebui publicai-openwebui
```

Save these commands for your future development workflow!