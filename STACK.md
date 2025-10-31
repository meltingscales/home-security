# Self-Hosted Home Security Stack

## Overview
This document outlines privacy-focused, fully self-hosted alternatives to Ring doorbell/camera systems. All options avoid third-party data processing and can operate completely locally without cloud dependencies.

**Current Setup**: This guide focuses on the **Reolink Video Doorbell PoE** (not other camera models). While other cameras are listed below for reference, our primary configuration uses the Reolink Video Doorbell PoE with Frigate NVR.

---

## Hardware Options

### Video Doorbell

#### **Reolink Video Doorbell PoE**
- **Price**: $80-130
- **Resolution**: 2K (5MP)
- **Storage**: microSD up to 256GB
- **Key Features**:
  - Full RTSP and ONVIF support
  - Excellent Frigate compatibility
  - PoE powered (no batteries)
  - Two-way audio
  - Color night vision
  - Local person detection
  - Multiple streams (main/sub)
- **Best For**: Best overall Frigate integration, reliable RTSP streams

---

### IP Cameras (Outdoor, Night Vision)

#### **Dahua IPC-HDW5442T-ZE** (Best Night Vision)
- **Price**: $130-180
- **Resolution**: 4MP (2688x1520)
- **Key Features**:
  - Exceptional night vision (Starlight sensor)
  - Full RTSP/ONVIF support
  - Varifocal lens (2.7-13.5mm)
  - PoE powered
  - Rock-solid Frigate compatibility
  - Multiple configurable streams
  - IR range up to 60m
- **Best For**: Users prioritizing excellent night performance

#### **Hikvision DS-2CD2387G2-LU (ColorVu)**
- **Price**: $150-200
- **Resolution**: 4K (8MP)
- **Key Features**:
  - 24/7 color night vision
  - Full RTSP/ONVIF support
  - Built-in white LED
  - PoE powered
  - Excellent Frigate compatibility
  - Multiple streams
  - Weatherproof (IP67)
- **Best For**: Users wanting color night vision without floodlights

#### **Reolink RLC-810A** (Budget Option)
- **Price**: $80-100
- **Resolution**: 4K (8MP)
- **Key Features**:
  - RTSP/ONVIF support
  - PoE powered
  - Built-in AI person/vehicle detection
  - IR night vision up to 30m
  - Works with Frigate (some configuration needed)
- **Best For**: Budget-conscious users
- **Note**: Night vision performance not as good as Dahua/Hikvision

#### **Amcrest IP8M-T2599EW** (Wide Angle)
- **Price**: $120-150
- **Resolution**: 4K (8MP)
- **Key Features**:
  - 112° wide angle lens
  - Full RTSP/ONVIF support
  - PoE powered
  - Color night vision
  - Good Frigate compatibility
  - Weatherproof (IP67)
- **Best For**: Users needing wide coverage area

---

### Floodlight Cameras

#### **Reolink Duo Floodlight PoE** (Recommended)
- **Price**: $200-250
- **Resolution**: 4K (8MP) dual-lens
- **Key Features**:
  - 180° panoramic view
  - Full RTSP/ONVIF support
  - Excellent Frigate compatibility
  - 2600 lumen LED floodlight
  - PoE powered
  - Two-way audio
  - Color night vision
  - Local AI detection
  - Multiple streams (main/sub/mid)
- **Best For**: Best overall floodlight camera for Frigate

#### **Reolink Elite Floodlight WiFi**
- **Price**: $180-230
- **Resolution**: 4K (8MP) dual-lens
- **Key Features**:
  - 180° panoramic view
  - Wi-Fi 6 + RTSP/ONVIF support
  - 3000 lumen floodlight
  - Proven Frigate compatibility
  - Color night vision with floodlight
  - Local AI video search
  - Two-way audio
- **Best For**: Users preferring WiFi over PoE

#### **Foscam FLC**
- **Price**: $150-180
- **Resolution**: 2K (4MP)
- **Key Features**:
  - RTSP/ONVIF support
  - 2600 lumen LED floodlight
  - 121° viewing angle
  - Dual-band WiFi
  - Two-way audio
  - AI person detection
  - Siren alarm
- **Best For**: Budget floodlight option with RTSP support

---

## Software Stack: Frigate NVR

```
Hardware: Compatible doorbell/camera with RTSP
         + Mini PC (Beelink EQ14 N150 recommended - Frigate Developer's current favorite)
         + Storage drive (4TB HDD over USB-C, ~$80)
         + Google Coral TPU ($60)

Software: Frigate NVR (free & open source)
         + Home Assistant (for notifications & automation)

Network: Standard network setup
```

**Why Frigate?**
- Completely free and open source
- Excellent AI object detection with Coral TPU
- Active community support
- Highly customizable
- 24/7 recording with intelligent retention
- Native Home Assistant integration
- Modern web UI
- Push notifications to your phone
- Low resource usage

**What You Get**:
- Real-time person/vehicle/animal detection
- 24/7 continuous recording
- Motion-activated clips
- Web dashboard for viewing live feeds and recordings
- Mobile notifications when someone's at the door
- Complete local control - no cloud dependencies

**Total Cost**: ~$320-495 one-time (hardware only, no subscriptions)

---

## What is Frigate?

**Frigate** is a complete and fully open-source NVR designed for Home Assistant with AI object detection. It uses local processing to analyze camera feeds in real-time.

### Key Features:
- **Local AI processing**: All detection runs on your hardware via Google Coral TPU
- **RTSP/ONVIF support**: Works with any IP camera
- **Real-time object detection**: People, vehicles, animals, and custom objects
- **24/7 recording**: Continuous recording with intelligent retention
- **Low resource usage**: Offloads AI to dedicated Coral TPU
- **Native Home Assistant integration**: First-class HA support
- **Free and open source**: No subscriptions or licensing costs

### Camera Support:
- ✅ Works with any RTSP/ONVIF camera
- ✅ Excellent support for Dahua, Hikvision, Reolink, Amcrest
- ✅ Generic RTSP streams from any brand
- ✅ Multiple configurable stream options (main/sub)

### Why Frigate?
- **vs Commercial NVRs**: No vendor lock-in, no subscriptions, complete control
- **vs ZoneMinder**: Modern interface, better AI detection, lower resource usage
- **vs Cloud solutions**: Complete privacy, no data leaves your network

**Best used**: As a complete NVR solution with Home Assistant for full home automation

---

## Recommended Complete Stacks

### Entry-Level Setup (Best Value):
```
Doorbell:        Reolink Video Doorbell PoE ($110)
Server:          Beelink EQ14 N150 Mini PC ($200)
Storage:         4TB HDD over USB-C ($80)
TPU:             Google Coral USB ($60)
Software:        Frigate NVR (free)
                 + Home Assistant (free)

Total: ~$450 one-time (no subscriptions ever)
```

**Includes:**
- 24/7 recording with AI detection
- Push notifications to phone
- Web dashboard + mobile app access
- ~90 days of 2K footage storage
- Complete home automation platform
- Excellent Frigate compatibility

---

### Multi-Camera Setup (3-4 Cameras):
```
Doorbell:        Reolink Video Doorbell PoE ($110)
IP Cameras:      2x Dahua IPC-HDW5442T-ZE ($320)
Floodlight:      Reolink Duo Floodlight PoE ($225)
Server:          Beelink EQ14 N150 Mini PC (8GB RAM) ($220)
Storage:         2TB NVMe SSD ($120)
TPU:             Google Coral USB ($60)
PoE Switch:      8-port PoE switch ($80)
Software:        Frigate NVR (free)
                 + Home Assistant (free)

Total: ~$1,135 one-time
```

**Includes:**
- Full property coverage (4 cameras)
- Professional-grade night vision
- 180° floodlight coverage
- 30+ days of 4K footage
- All cameras PoE powered
- Complete automation platform

---

### Budget-Conscious Setup:
```
Doorbell:        Reolink Video Doorbell PoE ($110)
IP Camera:       Reolink RLC-810A ($90)
Server:          Beelink EQ14 N150 Mini PC ($200)
Storage:         2TB HDD over USB-C ($50)
TPU:             Google Coral USB ($60)
PoE Injector:    2-port PoE injector ($25)
Software:        Frigate NVR (free)
                 + Home Assistant (free)

Total: ~$535 one-time
```

**Good for:**
- Small properties
- Budget-conscious users
- Testing Frigate before expanding

---

### Already Have Home Assistant?
```
Additional Cost: Cameras ($80-180 each)
                 + Google Coral TPU ($60)
                 + Storage (if needed)
                 + PoE switch/injectors ($25-80)

Total: Starting at ~$165+
```

**Note**:
- Beelink EQ14 N150 can handle 8-10 cameras with Coral TPU
- PoE cameras simplify wiring (power + data in one cable)
- All recommended hardware has proven Frigate compatibility
- Beelink is the Frigate Developer's current favorite brand for mini PCs

---

## Network Security Configuration

To ensure complete privacy:

1. **Block Camera Internet Access** (CRITICAL):
   - **Block the Reolink Video Doorbell PoE from accessing the internet**
   - Configure firewall rules at your router to prevent outbound internet traffic from the camera
   - Allow only local network communication (for RTSP streams to Frigate)
   - This prevents any telemetry, phone-home attempts, or data exfiltration to Reolink servers
   - Example router rule: Block all WAN traffic from camera IP (192.168.1.50)

2. **Standard Network Setup**:
   - Use regular home network (no VLAN required)
   - Cameras operate fully locally
   - All processing happens on your NVR server

3. **DNS Blocking** (Additional Layer):
   - Block manufacturer domains at router/Pi-hole
   - Prevents any phone-home attempts
   - Example domains to block: `*.reolink.com`, `*.reolink.host`

4. **Firmware**:
   - Keep firmware updated for security patches
   - Download firmware directly from manufacturer and update locally
   - Most modern cameras support standard RTSP/ONVIF protocols

---

## Key Advantages Over Ring

| Feature | Ring | Self-Hosted |
|---------|------|-------------|
| **Data sharing** | Sold to law enforcement | Never leaves your network |
| **Subscription** | $4-20/month required | $0 (completely free) |
| **Works offline** | No | Yes |
| **Your data** | Amazon owns it | You own it |
| **AI Processing** | Cloud | Local on your hardware |
| **Storage limits** | 60-180 days | Unlimited (your drives) |
| **Privacy** | Poor | Complete |

---

## Why Frigate Over Other NVRs?

Frigate is purpose-built for local, privacy-focused home security:

**vs Commercial NVRs (Blue Iris, etc.)**:
- Free and open source (no licensing)
- Lower resource usage
- No vendor lock-in
- Active development and community

**vs Traditional Open Source (ZoneMinder)**:
- Modern interface and design
- Better AI detection out of the box
- Lower CPU usage with Coral TPU
- Easier Home Assistant integration

**vs Cloud Solutions (Ring, Nest, Arlo)**:
- Complete privacy - no data leaves your network
- No subscriptions
- Unlimited storage (your hardware)
- No third-party access to your footage

---

## Hardware Requirements

### Minimum (1-2 cameras):
- **CPU**: Beelink EQ14 N150 or Raspberry Pi 4
- **RAM**: 4GB
- **Storage**: 500GB per camera for 30 days
- **TPU**: Google Coral USB (required for real-time detection)
- **Power**: ~20W total (server + cameras)

### Recommended (3-6 cameras):
- **CPU**: Beelink EQ14 N150 (recommended: 8GB model)
- **RAM**: 8GB
- **Storage**: 1TB per camera for 30 days
- **TPU**: Google Coral USB (essential)
- **Network**: PoE switch for PoE cameras
- **Power**: ~40-60W total (server + cameras + switch)

---

### Power Consumption

**Server:**
- Beelink EQ14 N150 Mini PC: ~10-15W idle, ~20-25W under load
- Raspberry Pi 4: ~3-5W idle, ~6-8W under load
- Google Coral USB TPU: ~2-3W

**Cameras (PoE):**
- 1080p camera: ~3-5W
- 2K camera: ~4-6W
- 4K camera: ~6-10W
- Floodlight camera: ~8-15W (without floodlight active)

**Network:**
- PoE switch (8-port): ~10-20W + camera power passthrough

**Example Total Power Draw:**
- Entry setup (1 doorbell): ~18-25W
- Multi-camera setup (4 cameras): ~50-70W
- Large setup (8 cameras): ~90-120W

**UPS Recommendations:**
For backup power during outages:
- **Entry setup**: 600VA/360W UPS (~4-6 hours runtime)
- **Multi-camera**: 1000VA/600W UPS (~3-4 hours runtime)
- **Large setup**: 1500VA/900W UPS (~2-3 hours runtime)

### Storage Calculations:
- **1080p camera**: ~15-20GB/day (24/7 recording)
  - 30 days: ~500-600GB
  - 90 days: ~1.5TB
- **2K camera**: ~25-30GB/day
  - 30 days: ~800GB-1TB
  - 90 days: ~2.5TB
- **4K camera**: ~40-50GB/day
  - 30 days: ~1.2-1.5TB
  - 90 days: ~4TB

### Additional Hardware:

**PoE Switch** (if using PoE cameras):
- 4-port: $40-60
- 8-port: $80-120
- 16-port: $150-250
- **Requirement**: Gigabit (1000 Mbps) recommended for 3+ cameras

**Alternative: PoE Injectors**
- Single port: $10-15 each
- Good for 1-2 cameras
- Cheaper than switch for small setups

---

### Network Bandwidth Requirements

**Per Camera (approximate):**
- **1080p main stream**: 2-4 Mbps
- **2K main stream**: 4-6 Mbps
- **4K main stream**: 8-12 Mbps
- **Sub streams**: 0.5-1 Mbps each

**Total Bandwidth Examples:**
- **2 cameras (2K)**: ~10-14 Mbps total
- **4 cameras (2K)**: ~20-28 Mbps total
- **6 cameras (4K)**: ~50-75 Mbps total

**Network Recommendations:**
- **Gigabit ethernet** (1000 Mbps) required for 3+ cameras
- **Cat5e or Cat6** cabling for PoE cameras
- Cameras → PoE Switch → Server on same network segment
- Avoid WiFi for continuous recording (unreliable, bandwidth issues)

**Router Requirements:**
- Supports static IP assignment
- Sufficient ports or need a switch
- For remote access: Port forwarding or VPN support

---

## Complete Setup Guide

### Step 1: Install Doorbell Hardware

1. **Wire the doorbell**:
   - Connect via PoE (Power over Ethernet)
   - Insert microSD card for local backup storage
   - Power on and connect to your network

2. **Configure network**:
   - Set static IP in your router (e.g., 192.168.1.50)
   - Note down IP address and admin credentials
   - Find RTSP stream URL in camera settings

**Common RTSP URL Formats:**

**Reolink Cameras:**
```
Main Stream:  rtsp://admin:password@192.168.1.50:554/h264Preview_01_main
Sub Stream:   rtsp://admin:password@192.168.1.50:554/h264Preview_01_sub
```

**Amcrest/Dahua Cameras:**
```
Main Stream:  rtsp://admin:password@192.168.1.50:554/cam/realmonitor?channel=1&subtype=0
Sub Stream:   rtsp://admin:password@192.168.1.50:554/cam/realmonitor?channel=1&subtype=1
```

**Hikvision Cameras:**
```
Main Stream:  rtsp://admin:password@192.168.1.50:554/Streaming/Channels/101
Sub Stream:   rtsp://admin:password@192.168.1.50:554/Streaming/Channels/102
```

**Test RTSP stream:**
```bash
vlc rtsp://admin:password@192.168.1.50:554/h264Preview_01_main
```

---

### Step 2: Install Home Assistant

**Option A: Home Assistant OS (Recommended for Beginners)**

1. Download Home Assistant OS image for your hardware
2. Flash to USB/SSD using Balena Etcher
3. Boot Beelink EQ14 N150 from the drive
4. Wait 20 minutes for initial setup
5. Access at `http://homeassistant.local:8123`

**Option B: Docker Compose (More Flexible)**

```bash
# Install Docker
curl -fsSL https://get.docker.com | sh

# Create docker-compose.yml
version: '3'
services:
  homeassistant:
    container_name: homeassistant
    image: ghcr.io/home-assistant/home-assistant:stable
    volumes:
      - ./homeassistant:/config
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped
    privileged: true
    network_mode: host

# Start Home Assistant
docker-compose up -d
```

**Initial Setup:**
- Open `http://YOUR_SERVER_IP:8123`
- Create admin account
- Set up location and timezone
- Install Home Assistant mobile app on your phone

---

### Step 3: Install Frigate NVR

**Via Home Assistant Add-on (If using HA OS):**
1. Go to Settings → Add-ons → Add-on Store
2. Search for "Frigate"
3. Click Install
4. Configure and start

**Via Docker Compose:**

```bash
# Add to docker-compose.yml
  frigate:
    container_name: frigate
    privileged: true
    restart: unless-stopped
    image: ghcr.io/blakeblackshear/frigate:stable
    shm_size: "256mb"
    devices:
      - /dev/bus/usb:/dev/bus/usb  # For Google Coral
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - ./frigate/config:/config
      - ./frigate/storage:/media/frigate
      - type: tmpfs
        target: /tmp/cache
        tmpfs:
          size: 1000000000
    ports:
      - "5000:5000"
    environment:
      FRIGATE_RTSP_PASSWORD: "your_password"

# Start Frigate
docker-compose up -d
```

---

### Step 4: Configure Frigate

Create `config/config.yml`:

```yaml
mqtt:
  enabled: False  # Enable later for notifications

detectors:
  coral:
    type: edgetpu
    device: usb

cameras:
  doorbell:
    ffmpeg:
      inputs:
        - path: rtsp://username:password@192.168.1.50:554/stream
          roles:
            - detect
            - record
    detect:
      width: 1920
      height: 1080
      fps: 5
    record:
      enabled: True
      retain:
        days: 30
        mode: all
      events:
        retain:
          default: 30
          mode: active_objects
    snapshots:
      enabled: True
      retain:
        default: 30
    objects:
      track:
        - person
        - car
    zones:
      doorway:
        coordinates: 640,0,1280,0,1280,720,640,720  # Adjust for your view

go2rtc:
  streams:
    doorbell:
      - rtsp://username:password@192.168.1.50:554/stream
```

Access Frigate at `http://YOUR_SERVER_IP:5000`

---

### Step 5: Setup Google Coral TPU

1. **Connect Coral USB to server**
2. **Install drivers** (if on bare metal):
   ```bash
   echo "deb https://packages.cloud.google.com/apt coral-edgetpu-stable main" | sudo tee /etc/apt/sources.list.d/coral-edgetpu.list
   curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   sudo apt-get update
   sudo apt-get install libedgetpu1-std
   ```
3. **Restart Frigate**
4. **Verify**: Check Frigate logs for "coral detector" initialization

---

### Step 6: Integrate Frigate with Home Assistant

1. **In Home Assistant:**
   - Go to Settings → Devices & Services
   - Click "+ Add Integration"
   - Search "Frigate"
   - Enter Frigate URL: `http://localhost:5000` (or server IP)
   - Configure camera entities

2. **Enable MQTT** (for notifications):
   - Install Mosquitto MQTT broker (HA Add-on or Docker)
   - Update Frigate config:
     ```yaml
     mqtt:
       enabled: True
       host: homeassistant.local  # or IP
       port: 1883
     ```

---

### Step 7: Setup Phone Notifications

1. **Install Home Assistant mobile app** on your phone
2. **Enable notifications** in app settings
3. **Install Frigate Notification Blueprint**:
   - Visit: https://community.home-assistant.io/t/frigate-mobile-app-notifications-2-0/559732
   - Click "Import Blueprint"
   - Configure:
     - Select camera: doorbell
     - Select device: Your phone
     - Enable snapshots and clips

4. **Test**: Walk in front of doorbell

**You'll now receive notifications with:**
- Snapshot of person detected
- Time and camera name
- Buttons to view clip or live feed

---

### Step 8: Create Dashboard (Optional)

In Home Assistant:
1. Go to Overview → Edit Dashboard
2. Add cards:
   - **Picture Glance Card**: Live doorbell view
   - **History Graph**: Detection events
   - **Frigate Card** (via HACS): Advanced view with events

Example:
```yaml
type: picture-glance
title: Front Door
camera_image: camera.doorbell
entities:
  - binary_sensor.doorbell_person_detected
  - binary_sensor.doorbell_motion
```

---

## Resources

### Documentation:
- **Frigate NVR**: https://docs.frigate.video/
- **Home Assistant**: https://www.home-assistant.io/
- **Google Coral TPU**: https://coral.ai/docs/accelerator/get-started/
- **MQTT (Mosquitto)**: https://mosquitto.org/

### Communities:
- r/homeassistant - General HA discussion
- r/frigate - Frigate-specific help
- r/selfhosted - Self-hosting community
- Home Assistant Community Forums - Best for detailed help
- IP Cam Talk forums - Camera hardware discussions

### Key Guides:
- Frigate Installation & Configuration: https://docs.frigate.video/
- Home Assistant Getting Started: https://www.home-assistant.io/getting-started/
- Frigate + Home Assistant Integration: https://docs.frigate.video/integrations/home-assistant/
- Frigate Notification Blueprint: https://community.home-assistant.io/t/frigate-mobile-app-notifications-2-0/559732
- Google Coral USB Setup: https://coral.ai/docs/accelerator/get-started/

---

## Future Expansion

All these stacks can easily expand to:
- Additional cameras (indoor/outdoor)
- License plate recognition (local)
- Facial recognition (local)
- Multiple doorbells
- Integration with alarm systems
- Local voice announcements

The infrastructure is the same - just add more cameras to your existing setup.
