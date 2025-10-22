# Quick Start Guide

## First Time Setup

```bash
# 1. Copy environment file
cp .env.example .env

# 2. Edit your timezone and password
nano .env

# 3. Start the stack
docker-compose up -d

# 4. Check logs
docker-compose logs -f
```

## Access Your Services

- **Home Assistant**: http://localhost:8123
- **Frigate**: http://localhost:8971

## When Your Doorbell Arrives

1. Connect doorbell to network via PoE
2. Find its IP address and set it to static (e.g., 192.168.1.50)
3. Edit `frigate/config/config.yml` and uncomment the doorbell section
4. Update the RTSP URLs with your doorbell's IP and password
5. Restart: `docker-compose restart frigate`

## Useful Commands

```bash
# View logs
docker-compose logs -f

# Restart a service
docker-compose restart frigate

# Stop everything
docker-compose down

# Update images
docker-compose pull && docker-compose up -d
```

## Full Documentation

See [DOCKER_SETUP.md](DOCKER_SETUP.md) for complete setup instructions.
