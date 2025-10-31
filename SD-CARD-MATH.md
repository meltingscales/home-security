# SD Card Storage Math for IP Cameras

## Why Use SD Cards?

SD cards provide **local backup storage** directly in your IP cameras. This is critical for:

1. **Network Failure Protection**: If your network goes down, cameras continue recording to the SD card
2. **NVR Failure Backup**: If your Frigate server crashes or loses power, you still have footage
3. **Redundancy**: Belt-and-suspenders approach - footage exists in two places
4. **Retrieval**: Can pull SD card and review footage directly if NVR is unavailable

**Important**: SD cards are NOT a replacement for your NVR - they're emergency backup only. Most cameras will loop/overwrite oldest footage when the card fills up.

---

## Storage Calculations by Resolution

### Reolink Video Doorbell PoE (2K / 5MP)
- **Bitrate**: ~4-6 Mbps (varies with motion/complexity)
- **Average**: ~5 Mbps = 0.625 MB/s
- **Per Day**: ~54 GB (24/7 recording)

| SD Card Size | Days of 24/7 Footage | Notes |
|--------------|---------------------|--------|
| 32 GB | ~0.6 days (14 hours) | Too small, avoid |
| 64 GB | ~1.2 days (29 hours) | Minimum acceptable |
| 128 GB | ~2.4 days | Good for short outages |
| 256 GB | ~4.7 days | **Recommended** |
| 512 GB | ~9.5 days | Maximum overkill |

**Recommended**: **256 GB** - Provides ~5 days of backup footage

---

### Reolink Duo Floodlight PoE (4K / 8MP Dual-Lens)
- **Bitrate**: ~8-12 Mbps (dual 180° streams)
- **Average**: ~10 Mbps = 1.25 MB/s
- **Per Day**: ~108 GB (24/7 recording)

| SD Card Size | Days of 24/7 Footage | Notes |
|--------------|---------------------|--------|
| 64 GB | ~0.6 days (14 hours) | Too small |
| 128 GB | ~1.2 days (29 hours) | Bare minimum |
| 256 GB | ~2.4 days | Acceptable |
| 512 GB | ~4.7 days | **Recommended** |
| 1 TB | ~9.3 days | Excessive but future-proof |

**Recommended**: **512 GB** - Provides ~5 days of backup footage

---

### Standard IP Cameras (4K / 8MP)
- **Bitrate**: ~6-10 Mbps (single stream)
- **Average**: ~8 Mbps = 1 MB/s
- **Per Day**: ~86 GB (24/7 recording)

| SD Card Size | Days of 24/7 Footage | Notes |
|--------------|---------------------|--------|
| 64 GB | ~0.7 days (17 hours) | Too small |
| 128 GB | ~1.5 days | Minimum |
| 256 GB | ~3 days | Good balance |
| 512 GB | ~6 days | **Recommended** |

**Recommended**: **256-512 GB** depending on budget

---

## Quick Reference Table

| Camera Type | Recommended Size | Backup Duration | Cost (approx) |
|-------------|------------------|-----------------|---------------|
| 2K Doorbell | 256 GB | ~5 days | $20-30 |
| 4K Floodlight | 512 GB | ~5 days | $35-50 |
| 4K IP Camera | 256-512 GB | 3-6 days | $20-50 |
| 1080p Camera | 128-256 GB | 4-8 days | $15-30 |

---

## SD Card Recommendations

### Endurance Matters
Regular SD cards will **fail quickly** with continuous recording. Use cards rated for:
- **High Endurance** (designed for dashcams/security cameras)
- **Write cycles**: 10,000+ hours rated
- **Temperature range**: -25°C to 85°C

### Recommended SD Cards (in order of preference):

1. **Samsung PRO Endurance** (Best)
   - Rated for continuous recording
   - 5-year warranty
   - Sizes: 32GB-256GB

2. **SanDisk High Endurance** (Great value)
   - Designed for video surveillance
   - Good reliability
   - Sizes: 32GB-256GB

3. **Western Digital Purple** (Surveillance-specific)
   - Made for security cameras
   - Excellent durability
   - Sizes: 64GB-512GB

**Avoid**: Generic/cheap SD cards from Amazon - they will fail fast with 24/7 recording.

---

## Real-World Scenarios

### Scenario 1: Network Outage (3 days)
Your router dies and takes 3 days to replace.

**Without SD cards**: You lose all footage from those 3 days
**With 256GB cards**: Cameras record locally, you recover all footage

---

### Scenario 2: NVR Server Failure (1 week)
Your Frigate server's drive fails and you need to rebuild.

**Without SD cards**: No recordings during rebuild
**With 512GB cards**: Last 5-6 days preserved on cameras

---

### Scenario 3: Power Outage (12 hours)
Power outage takes down your network but cameras stay up (PoE switch on UPS).

**Without SD cards**: Cameras are isolated, no recording
**With any SD card**: Cameras continue recording independently

---

## Cost-Benefit Analysis

### Total Cost for Full Setup:
- **Doorbell**: 1x 256GB card = $25
- **Floodlight**: 1x 512GB card = $45
- **4x IP Cameras**: 4x 256GB cards = $100

**Total**: ~$170 for complete backup redundancy

### Is it worth it?
**Yes, if**:
- You have unreliable network/power
- Cameras monitor critical areas (entry points, valuables)
- Peace of mind is worth $170

**Maybe not, if**:
- Your network is rock-solid and on UPS
- Your Frigate server has redundant storage (RAID)
- Budget is extremely tight

---

## Setup Tips

1. **Format in camera**: Always format SD cards using the camera's web interface, not your computer
2. **Check regularly**: Most cameras show SD card health in settings - check monthly
3. **Enable overwrite**: Ensure "loop recording" is enabled so old footage is overwritten when full
4. **Test it**: Disconnect camera from network and verify it's recording to SD card
5. **Label cards**: If you pull a card, label it with camera name and date range

---

## Common Questions

### Q: Can I use the SD card as primary storage instead of Frigate?
**A**: No. SD cards will fail eventually with continuous writes, and you lose all AI detection, notifications, and central management. Always use Frigate as primary, SD as backup.

### Q: Do I need SD cards if my Frigate server has RAID?
**A**: RAID protects against drive failure, not network failure. SD cards protect against network issues.

### Q: How often do SD cards fail?
**A**: High-endurance cards typically last 1-3 years with 24/7 recording. Regular cards fail in weeks/months.

### Q: Can I recover footage from SD card if camera dies?
**A**: Yes, pull the SD card and read it on any computer with an SD card reader.

### Q: Do all IP cameras support SD cards?
**A**: Most modern IP cameras do, but check specs. All recommended Reolink cameras support microSD up to 256GB-512GB.

---

## Bottom Line

**Recommended SD Card Setup**:
- **Reolink Video Doorbell PoE**: 256 GB high-endurance (~5 days backup)
- **Reolink Duo Floodlight PoE**: 512 GB high-endurance (~5 days backup)
- **Additional IP Cameras**: 256 GB high-endurance each (~3-5 days backup)

**Total investment**: $25-50 per camera for invaluable peace of mind and network failure protection.
