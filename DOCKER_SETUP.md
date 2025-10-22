# Docker Setup Guide for Frigate + Home Assistant

This guide will help you set up Frigate NVR and Home Assistant on your desktop for testing your home security stack.

## Prerequisites

- Docker and Docker Compose installed
- Google Coral USB TPU (optional for initial testing, required for AI detection)
- Your Reolink Video Doorbell PoE (when it arrives)

## Quick Start

### 1. Initial Setup

```bash
# Copy environment file and customize
cp .env.example .env

# Edit .env with your settings
nano .env
```

Edit the `.env` file:
- Set your timezone (e.g., `TZ=America/New_York`)
- Set a secure RTSP password

### 2. Start the Stack

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# View specific service logs
docker-compose logs -f frigate
docker-compose logs -f homeassistant
```

### 3. Access the Services

After starting (wait 2-3 minutes for initial setup):

- **Home Assistant**: http://localhost:8123
- **Frigate**: http://localhost:8971
- **MQTT Broker**: localhost:1883 (internal only)

## Initial Configuration

### Home Assistant Setup

1. Open http://localhost:8123
2. Create your admin account
3. Set up your location and timezone
4. Install the Home Assistant mobile app (optional)

### Frigate Setup

1. Open http://localhost:8971
2. Frigate should start with the default config
3. Wait for your doorbell to arrive to add camera configuration

### Connect Google Coral TPU (When Available)

1. Plug USB Coral directly into motherboard USB port (avoid hubs)
2. Restart Frigate: `docker-compose restart frigate`
3. Check logs: `docker-compose logs frigate | grep coral`
4. You should see: "coral detector started"

## Configure Your Reolink Doorbell (When It Arrives)

### Step 1: Set Up Doorbell on Network

1. Install doorbell with PoE connection
2. Find its IP address (check your router or use Reolink app)
3. Set a static IP in your router (e.g., 192.168.1.50)
4. Note down the admin password

### Step 2: Find RTSP Stream URL

Access your doorbell's web interface and find RTSP settings.

**Reolink RTSP URLs:**
- Main stream: `rtsp://admin:YOUR_PASSWORD@192.168.1.50:554/h264Preview_01_main`
- Sub stream: `rtsp://admin:YOUR_PASSWORD@192.168.1.50:554/h264Preview_01_sub`

### Step 3: Configure Frigate

Edit `frigate/config/config.yml` and uncomment the doorbell section:

```yaml
cameras:
  doorbell:
    enabled: true
    ffmpeg:
      inputs:
        - path: rtsp://admin:YOUR_PASSWORD@192.168.1.50:554/h264Preview_01_main
          roles:
            - record
        - path: rtsp://admin:YOUR_PASSWORD@192.168.1.50:554/h264Preview_01_sub
          roles:
            - detect
    detect:
      enabled: true
      width: 640
      height: 480
      fps: 5
    record:
      enabled: true
      retain:
        days: 30
        mode: all
    objects:
      track:
        - person
        - car
```

Replace:
- `YOUR_PASSWORD` with your doorbell password
- `192.168.1.50` with your doorbell's IP address

### Step 4: Restart Frigate

```bash
docker-compose restart frigate
```

Check logs to verify camera connection:
```bash
docker-compose logs -f frigate
```

You should see: "doorbell: ffmpeg sent a broken frame"... followed by successful frame processing.

## Integrate Frigate with Home Assistant

### Step 1: Install MQTT Integration in Home Assistant

1. Go to Settings → Devices & Services
2. Click "+ ADD INTEGRATION"
3. Search for "MQTT"
4. Configure:
   - Broker: `mosquitto` (or `localhost`)
   - Port: `1883`
   - Leave username/password empty (anonymous access)
5. Click Submit

### Step 2: Install Frigate Integration

1. Go to Settings → Devices & Services
2. Click "+ ADD INTEGRATION"
3. Search for "Frigate"
4. Configure:
   - URL: `http://frigate:8971` (if using host network, use `http://localhost:8971`)
5. Click Submit

Your cameras will now appear in Home Assistant!

## Set Up Notifications (Optional)

### Step 1: Install Home Assistant Mobile App

- iOS: Download from App Store
- Android: Download from Google Play

### Step 2: Enable Notifications in App

1. Open app and log in
2. Go to Settings → Notifications
3. Enable notifications

### Step 3: Install Frigate Notification Blueprint

1. Visit: https://community.home-assistant.io/t/frigate-mobile-app-notifications-2-0/559732
2. Click "Import Blueprint" button
3. In Home Assistant:
   - Go to Settings → Automations & Scenes → Blueprints
   - Find "Frigate Mobile App Notifications"
   - Click "Create Automation"
   - Configure:
     - Camera: doorbell
     - Mobile device: Your phone
     - Enable snapshots and clips
4. Save automation

You'll now receive notifications when someone is detected at your door!

## Useful Commands

```bash
# Start services
docker-compose up -d

# Stop services
docker-compose down

# Restart a specific service
docker-compose restart frigate

# View logs
docker-compose logs -f

# View logs for specific service
docker-compose logs -f frigate

# Update to latest versions
docker-compose pull
docker-compose up -d

# Check service status
docker-compose ps

# Access container shell (for debugging)
docker exec -it frigate bash
```

## Storage Management

### Check Storage Usage

```bash
# Check Frigate storage
du -sh frigate/storage/

# Check recording storage
du -sh frigate/storage/recordings/

# View by camera
du -sh frigate/storage/recordings/*
```

### Adjust Retention

Edit `frigate/config/config.yml`:

```yaml
record:
  enabled: true
  retain:
    days: 30  # Change this value
    mode: all
```

Then restart Frigate: `docker-compose restart frigate`

## Troubleshooting

### Frigate "Bus error" crashes

Increase shared memory in `docker-compose.yml`:
```yaml
shm_size: "1gb"  # or "2gb"
```

### Google Coral not detected

1. Ensure USB Coral is plugged directly into motherboard (not through hub)
2. Check device is visible: `lsusb | grep Coral`
3. Restart Frigate: `docker-compose restart frigate`
4. Check logs: `docker-compose logs frigate | grep coral`

### Camera won't connect

1. Verify camera IP: `ping 192.168.1.50`
2. Test RTSP stream: `vlc rtsp://admin:password@192.168.1.50:554/h264Preview_01_sub`
3. Check Frigate logs: `docker-compose logs -f frigate`
4. Verify credentials and URL format

### Home Assistant can't connect to Frigate

1. Check both services are running: `docker-compose ps`
2. Verify MQTT is working:
   - Settings → Devices & Services → MQTT
   - Check status is "Connected"
3. Try using IP address instead of service name: `http://localhost:8971`

### MQTT issues

Check MQTT logs:
```bash
docker-compose logs mosquitto
```

Test MQTT connection:
```bash
# Install mosquitto-clients if needed
sudo apt install mosquitto-clients

# Subscribe to test topic
mosquitto_sub -h localhost -t 'frigate/#' -v
```

## Hardware Acceleration (Optional)

### Intel Quick Sync (for Intel CPUs with iGPU)

Uncomment in `docker-compose.yml`:
```yaml
devices:
  - /dev/dri/renderD128:/dev/dri/renderD128
```

Update Frigate config:
```yaml
ffmpeg:
  hwaccel_args: preset-vaapi
```

## Security Considerations

### For Testing on Desktop
- This setup uses `allow_anonymous: true` for MQTT (fine for testing)
- Services are exposed on localhost

### For Production Deployment
1. Enable MQTT authentication
2. Use proper firewall rules
3. Consider using VPN for remote access
4. Block camera internet access (see STACK.md)

## Next Steps

1. ✅ Start the stack
2. ✅ Set up Home Assistant account
3. ⏳ Wait for doorbell to arrive
4. ⏳ Configure doorbell camera in Frigate
5. ⏳ Integrate with Home Assistant
6. ⏳ Set up mobile notifications
7. ⏳ Test person detection
8. ⏳ Configure zones and automation

## Resources

- **Frigate Documentation**: https://docs.frigate.video/
- **Home Assistant Docs**: https://www.home-assistant.io/
- **MQTT Integration**: https://www.home-assistant.io/integrations/mqtt/
- **Frigate Integration**: https://docs.frigate.video/integrations/home-assistant/
- **Community Forum**: https://community.home-assistant.io/

## Backup and Data

Your data is stored in these directories:
- `frigate/storage/` - Recordings and clips
- `frigate/config/` - Frigate configuration and database
- `homeassistant/` - Home Assistant configuration
- `mosquitto/data/` - MQTT persistence data

To backup, simply copy these directories to a safe location.
