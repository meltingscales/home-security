# Bandwidth & Storage Math for IP Camera Systems

## Why Use SD Cards?

SD cards provide **local backup storage** directly in your IP cameras. This is critical for:

1. **Network Failure Protection**: If your network goes down, cameras continue recording to the SD card
2. **NVR Failure Backup**: If your Frigate server crashes or loses power, you still have footage
3. **Redundancy**: Belt-and-suspenders approach - footage exists in two places
4. **Retrieval**: Can pull SD card and review footage directly if NVR is unavailable

**Important**: SD cards are NOT a replacement for your NVR - they're emergency backup only. Most cameras will loop/overwrite oldest footage when the card fills up.

---

## Network & Storage Bandwidth Requirements

### Your Current Stack Bandwidth Needs

**Hardware:**
- Reolink Video Doorbell PoE (2K / 5MP)
- Reolink Duo Floodlight PoE (4K / 8MP dual-lens)
- Beelink EQ14 N150 Mini PC
- 4TB HDD over USB 3.0/3.1

**Camera Bandwidth:**
- Doorbell (2K): 4-6 Mbps average = ~5 Mbps
- Floodlight (4K): 8-12 Mbps average = ~10 Mbps
- **Total Network Traffic**: ~15 Mbps (or ~1.875 MB/s)

**Storage Write Speed Required:**
- Recording both cameras 24/7: ~1.875 MB/s sustained write
- Daily storage: ~162 GB/day (54 GB doorbell + 108 GB floodlight)

---

### USB Bandwidth Analysis

#### USB 3.0 (Your Current Setup)
- **Theoretical Max**: 5 Gbps (640 MB/s)
- **Real-World Speed**: ~300-400 MB/s sustained
- **Your Requirement**: 1.875 MB/s
- **Overhead Available**: **160-213x more than needed**
- **Verdict**: ✅ **More than sufficient** - massively over-specced

#### USB 3.1 Gen 1 (5 Gbps)
- Same as USB 3.0
- **Overhead**: 160-213x more than needed
- **Verdict**: ✅ **More than sufficient** (identical to USB 3.0)

#### USB 3.1 Gen 2 (10 Gbps)
- **Theoretical Max**: 10 Gbps (1,280 MB/s)
- **Real-World Speed**: ~700-900 MB/s sustained
- **Your Requirement**: 1.875 MB/s
- **Overhead Available**: **373-480x more than needed**
- **Verdict**: ✅ **Extreme overkill** (unnecessary for 2 cameras)

**Bottom Line**: USB 3.0 is perfect for your 2-camera setup. Even with 10-15 cameras, USB 3.0 would still have plenty of headroom.

---

### Network Backbone Bandwidth Analysis (CAT6)

#### CAT6 Ethernet Specifications

**Standard 1 Gbps Mode** (up to 100m):
- **Theoretical Max**: 1 Gbps (1000 Mbps / 125 MB/s)
- **Real-World Speed**: ~900-950 Mbps practical throughput
- **Your Requirement**: 15 Mbps for 2 cameras
- **Overhead Available**: **60-63x more than needed**
- **Verdict**: ✅ **Excellent** - you could run 50+ cameras on 1 Gbps

**10 Gbps Mode** (up to 55m/180ft):
- **Theoretical Max**: 10 Gbps (10,000 Mbps / 1,250 MB/s)
- **Real-World Speed**: ~9,000-9,500 Mbps practical
- **Your Requirement**: 15 Mbps for 2 cameras
- **Overhead Available**: **600-633x more than needed**
- **Verdict**: ✅ **Massive overkill** (only needed for large deployments)

#### Cable Run Considerations

**For your 2-camera setup:**
- **Recommended**: CAT6 in standard 1 Gbps mode
- **Max distance**: 100m (328 feet) from switch to camera
- **Your bandwidth usage**: ~1.5% of available capacity

**Scaling up (hypothetical 10-camera setup):**
- 10x 4K cameras: ~100 Mbps total
- Still only 10% of 1 Gbps capacity
- CAT6 standard mode still excellent

---

### Complete System Bandwidth Map

```
[Cameras] --PoE/CAT6--> [PoE Switch] --CAT6--> [Beelink EQ14]
                                                      |
                                                   USB 3.0
                                                      |
                                                [4TB HDD Storage]

Camera Network (CAT6 @ 1 Gbps):
  - Doorbell: 5 Mbps    (0.5% capacity used)
  - Floodlight: 10 Mbps (1.0% capacity used)
  - Total: 15 Mbps      (1.5% capacity used)
  - Available: 985 Mbps (98.5% free)

Storage Write (USB 3.0 @ 5 Gbps):
  - Write speed needed: 1.875 MB/s
  - USB 3.0 real-world: 300-400 MB/s
  - Capacity used: <1%
  - Available: 99%+ free
```

---

### Bandwidth Bottleneck Analysis

**Potential Bottlenecks** (ranked by likelihood):

1. **Hard Drive Write Speed** ⚠️
   - 4TB HDD typical: 100-150 MB/s sustained
   - Your needs: 1.875 MB/s
   - **Status**: ✅ No issue (79-80x overhead)

2. **Network Switch Capacity**
   - Gigabit switch: 1000 Mbps
   - Your needs: 15 Mbps
   - **Status**: ✅ No issue (67x overhead)

3. **USB 3.0 Bandwidth**
   - USB 3.0: 300-400 MB/s real-world
   - Your needs: 1.875 MB/s
   - **Status**: ✅ No issue (160-213x overhead)

4. **Beelink CPU/RAM**
   - N150 processor + 8GB RAM
   - Handles 8-10 cameras easily with Coral TPU
   - Your setup: 2 cameras
   - **Status**: ✅ No issue (massively over-provisioned)

**Actual Bottleneck**: None. Your system is **massively over-provisioned** for 2 cameras.

---

### Expansion Capacity

**How many cameras can your current infrastructure handle?**

| Component | Current | 2 Cameras | 5 Cameras | 10 Cameras | Bottleneck |
|-----------|---------|-----------|-----------|------------|------------|
| **Network (CAT6 1Gbps)** | 1000 Mbps | 15 Mbps | 50 Mbps | 100 Mbps | ✅ (10x overhead) |
| **USB 3.0 Storage** | 5 Gbps | 15 Mbps | 50 Mbps | 100 Mbps | ✅ (50x overhead) |
| **HDD Write (4TB)** | 150 MB/s | 1.9 MB/s | 6.25 MB/s | 12.5 MB/s | ✅ (12x overhead) |
| **Beelink N150 CPU** | 8-10 cams | 2 cams | 5 cams | 10 cams | ✅ (at limit) |
| **Google Coral TPU** | 10-15 cams | 2 cams | 5 cams | 10 cams | ✅ (5 fps ea.) |

**Maximum Capacity**: Your current hardware can easily support **8-10 cameras** before hitting any bottlenecks (CPU/TPU would be the first limit).

---

### Upgrade Path (If Expanding)

**If you add 3-8 more cameras, you'll need:**

1. **Nothing immediately** - current infrastructure handles 10 cameras
2. **Larger PoE Switch** - if you run out of ports (need 8-16 port)
3. **More Storage** - add another 4TB drive via second USB 3.0 port (Beelink has multiple)
4. **Possible TPU Upgrade** - consider second Coral or PCIe Coral for 10+ cameras

**Cost to expand to 10 cameras**: ~$0-50 (just larger PoE switch if needed)

**Your network backbone (CAT6) and USB 3.0 storage interface need no upgrades for up to 10 cameras.**

---

## HDD Storage Duration & Lifespan Analysis

### Your 4TB Drive: How Long Does It Last?

**Your Current Setup (2 Cameras):**
- **Daily Recording**: 162 GB/day (54 GB doorbell + 108 GB floodlight)
- **4TB Drive Capacity**: ~3,725 GB usable (after formatting)
- **Retention Duration**: **~23 days** of continuous 24/7 recording

**Answer**: ✅ **4TB is good for 3+ weeks** of footage. This is reasonable for most home security needs.

---

### Storage Duration Comparison Chart

**For Your 2-Camera Setup** (162 GB/day @ 24/7 recording):

| Drive Size | Usable Capacity | Retention Time | Cost (approx) | Notes |
|------------|-----------------|----------------|---------------|-------|
| **2TB** | ~1,860 GB | ~11.5 days | $50-70 | Minimum viable |
| **4TB** | ~3,725 GB | **~23 days** | **$80-100** | ✅ **Current setup - Good** |
| **6TB** | ~5,590 GB | ~34.5 days | $120-150 | Better for high-activity areas |
| **8TB** | ~7,450 GB | ~46 days | $150-180 | 1.5 months retention |
| **10TB** | ~9,300 GB | ~57 days | $180-220 | 2 months retention |
| **12TB** | ~11,160 GB | ~69 days | $220-280 | Overkill for 2 cameras |

**Recommendation for 2 cameras**: **4-6TB** is the sweet spot for cost vs. retention.

---

### What If You Expand to More Cameras?

**3 Cameras** (2K doorbell + 4K floodlight + 4K IP camera):
- Daily: ~248 GB/day
- **4TB lasts**: ~15 days
- **6TB lasts**: ~22.5 days ✅ (recommended)

**5 Cameras** (add 2 more 4K cameras):
- Daily: ~420 GB/day
- **4TB lasts**: ~9 days
- **8TB lasts**: ~17.7 days ✅ (recommended)

**10 Cameras** (4x 2K + 6x 4K):
- Daily: ~860 GB/day
- **8TB lasts**: ~8.7 days
- **12TB lasts**: ~13 days
- **16TB lasts**: ~17.4 days ✅ (recommended)

**Rule of Thumb**: Aim for 14-30 days retention. Less than 14 days and you might miss important events if you're on vacation.

---

### HDD Lifespan & Health

#### Expected Lifespan (24/7 Surveillance Use)

**Consumer HDDs** (WD Blue, Seagate Barracuda):
- **Not recommended** for 24/7 recording
- Typical lifespan: 1-2 years under continuous writes
- Rated for 8x5 operation (8 hours/day, 5 days/week)

**Surveillance HDDs** (WD Purple, Seagate SkyHawk) ⭐ **Recommended**:
- **Designed for 24/7 operation**
- Expected lifespan: **3-5 years** under continuous writes
- Rated for 180 TB/year workload (or more)
- Optimized for streaming write patterns
- Better error recovery for video surveillance

**NAS HDDs** (WD Red, Seagate IronWolf):
- Good for 24/7 operation
- Expected lifespan: 3-5 years
- Higher cost than surveillance drives
- Optimized for RAID (not necessary for single-drive setups)

#### Your 2-Camera Setup Write Load

**Annual Write Volume**:
- 162 GB/day × 365 days = **59.1 TB/year**

**Drive Recommendation**:
| Drive Type | Rated Workload | Your Load | Lifespan Estimate | Verdict |
|------------|---------------|-----------|-------------------|---------|
| **Consumer HDD** | 55 TB/year | 59.1 TB/year | 1-2 years | ❌ Over spec |
| **WD Purple** | 180 TB/year | 59.1 TB/year | 3-5 years | ✅ **Ideal** |
| **Seagate SkyHawk** | 180 TB/year | 59.1 TB/year | 3-5 years | ✅ **Ideal** |
| **NAS Drive** | 180+ TB/year | 59.1 TB/year | 3-5 years | ✅ Overkill |

**Bottom Line**: Use **WD Purple** or **Seagate SkyHawk** for your 4TB drive. They're designed exactly for this workload.

---

### Recommended Surveillance HDDs

**WD Purple Series** (Optimized for Surveillance):
- **4TB WD Purple**: $80-100 (✅ perfect for your setup)
- **6TB WD Purple**: $120-140
- **8TB WD Purple**: $160-190
- Rated for 64 cameras, 180 TB/year workload
- 3-year warranty

**Seagate SkyHawk Series**:
- **4TB SkyHawk**: $80-105
- **6TB SkyHawk**: $115-135
- **8TB SkyHawk**: $150-180
- Rated for 64 cameras, 180 TB/year workload
- 3-year warranty
- ImagePerfect firmware for AI/NVR applications

**Either brand is excellent** - choose based on price and availability.

---

### HDD Health Monitoring

#### SMART Monitoring (Critical!)

Modern HDDs report health via SMART (Self-Monitoring, Analysis, and Reporting Technology). You should monitor this regularly.

**Key SMART Attributes to Watch**:
1. **Reallocated Sectors Count** - Should be 0 (any value means failing drive)
2. **Current Pending Sectors** - Should be 0
3. **Temperature** - Should be under 50°C (ideally 30-45°C)
4. **Power-On Hours** - Track drive age
5. **Uncorrectable Errors** - Should be 0

**How to Monitor on Linux**:
```bash
# Install smartmontools
sudo apt install smartmontools

# Check drive health (replace /dev/sda with your drive)
sudo smartctl -a /dev/sda

# Run short self-test
sudo smartctl -t short /dev/sda

# Check test results after 2 minutes
sudo smartctl -l selftest /dev/sda
```

**Set up automatic monitoring**:
```bash
# Enable smartd daemon
sudo systemctl enable smartd
sudo systemctl start smartd

# Configure email alerts in /etc/smartd.conf
```

**Home Assistant Integration**:
- Install "System Monitor" integration
- Monitor disk usage and health
- Set alerts when drive is >80% full
- Track temperature and SMART status

---

### When to Upgrade Storage

**Upgrade to larger drive if**:
1. **Retention < 14 days** - You might miss events during vacations
2. **Disk >80% full regularly** - System performance degrades
3. **Adding more cameras** - See expansion chart above
4. **SMART errors appear** - Replace immediately, drive is failing

**Upgrade to second drive if**:
1. **Want redundancy** - Mirror to second drive for backup
2. **Adding 5+ cameras** - Split load across two drives
3. **Different retention needs** - Long-term storage on second drive

**Your Beelink EQ14 N150 has multiple USB 3.0 ports** - you can easily add a second 4TB drive later without replacing the first.

---

### Storage Replacement Schedule

**Proactive Replacement** (recommended to avoid data loss):

| Drive Type | Replace After | Monitoring | Notes |
|------------|---------------|------------|-------|
| **WD Purple / SkyHawk** | 3-4 years | SMART monthly | Before warranty expires |
| **Consumer HDD** | 2 years | SMART weekly | Not recommended |
| **High-activity setup** | 2-3 years | SMART weekly | 8+ cameras or high bitrate |

**Reactive Replacement** (wait for SMART warnings):
- More risky - could lose footage
- Only if you have good backups (SD cards in cameras)
- Monitor SMART religiously

**Your Setup**: Plan to replace your 4TB surveillance drive every **3-4 years** for peace of mind.

---

### Quick Answer: Is 4TB Good Enough?

**For your 2-camera setup**:
- ✅ **Yes, 4TB is good** - provides ~23 days retention
- ✅ **Use WD Purple or Seagate SkyHawk** - designed for 24/7 recording
- ✅ **Well within workload limits** - only 59 TB/year vs 180 TB/year rated
- ✅ **Monitor SMART monthly** - catch failures before data loss
- ✅ **Plan to replace in 3-4 years** - proactive maintenance

**Consider 6TB if**:
- You want 30+ days retention (monthly review cycle)
- High-traffic areas with lots of motion (bitrates spike)
- Planning to add 1-2 more cameras soon

**Consider 8TB+ if**:
- Adding 4+ more cameras
- Want 60-90 day retention for legal/insurance purposes
- High-value property requiring extended footage

**Your current 4TB is solid for 2 cameras.**

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
