# HackRF Drone Detection System - Hardware Setup Guide

**Version:** 2.0.0  
**Last Updated:** 2024-01-15  
**Difficulty:** Intermediate  

---

## 📋 Table of Contents

1. [Hardware Overview](#hardware-overview)
2. [Required Components](#required-components)
3. [Optional Components](#optional-components)
4. [Antenna Selection Guide](#antenna-selection-guide)
5. [Assembly Instructions](#assembly-instructions)
6. [Connection Diagrams](#connection-diagrams)
7. [Power Requirements](#power-requirements)
8. [Mounting & Placement](#mounting--placement)
9. [Calibration Procedure](#calibration-procedure)
10. [Troubleshooting Hardware](#troubleshooting-hardware)
11. [Maintenance](#maintenance)
12. [Advanced Configurations](#advanced-configurations)

---

## 🔧 Hardware Overview

The HackRF Drone Detection System uses Software Defined Radio (SDR) technology to detect and identify drone RF signatures in real-time.

### System Block Diagram
┌─────────────────────────────────────────────────────────────────────────────┐
│ DRONE DETECTION SYSTEM │
├─────────────────────────────────────────────────────────────────────────────┤
│ │
│ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ │
│ │ 2.4 GHz │ │ 5.8 GHz │ │ 915 MHz │ │ 433 MHz │ │
│ │ Antenna │ │ Antenna │ │ Antenna │ │ Antenna │ │
│ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ │
│ │ │ │ │ │
│ └────────────────┼────────────────┼────────────────┘ │
│ │ │ │
│ ┌─────┴─────┐ ┌────┴─────┐ │
│ │ RF Switch │ │ Direct │ │
│ │ (Opt.) │ │ Cable │ │
│ └─────┬─────┘ └────┬─────┘ │
│ │ │ │
│ └────────┬─────────┘ │
│ │ │
│ ┌───────┴───────┐ │
│ │ HackRF One │ │
│ │ 10MHz-6GHz │ │
│ └───────┬───────┘ │
│ │ │
│ ┌───────┴───────┐ │
│ │ USB │ │
│ │ 3.0 Cable │ │
│ └───────┬───────┘ │
│ │ │
│ ┌───────┴───────┐ │
│ │ SBC Computer │ │
│ │ (Pi 4/NUC) │ │
│ └───────────────┘ │
│ │
└─────────────────────────────────────────────────────────────────────────────┘

text

---

## 📦 Required Components

### Core Components

| Component | Specification | Quantity | Estimated Cost | Purpose |
|-----------|--------------|----------|----------------|---------|
| **HackRF One** | 10MHz-6GHz, 20MSPS | 1 | $300-350 | RF signal capture |
| **Antenna (2.4GHz)** | Yagi, 15-20dBi | 1 | $40-80 | Drone control signals |
| **USB 3.0 Cable** | Type-A to Micro-B | 1 | $10-15 | Data transfer |
| **Single Board Computer** | Raspberry Pi 4 (4GB+) | 1 | $75-100 | Processing |
| **MicroSD Card** | 32GB Class 10 | 1 | $15-20 | OS & storage |
| **Power Supply** | 5V/3A USB-C | 1 | $10-15 | SBC power |
| **SMA Cables** | RG316, 30cm | 2-4 | $5-10 each | RF connections |

### Recommended SBC Options

| Model | CPU | RAM | USB | Price | Recommendation |
|-------|-----|-----|-----|-------|----------------|
| **Raspberry Pi 4** | Quad-core 1.5GHz | 4-8GB | USB 3.0 | $75 | ⭐ Best value |
| **Intel NUC** | i3/i5 | 8GB+ | USB 3.1 | $300+ | ⭐ Best performance |
| **Orange Pi 5** | Octa-core | 4-16GB | USB 3.0 | $80 | ⭐ Good alternative |
| **Rock Pi 4** | Hexa-core | 4GB | USB 3.0 | $100 | Good alternative |

---

## 🎛 Optional Components

### Enhanced Detection

| Component | Specification | Purpose | Cost |
|-----------|--------------|---------|------|
| **Extra Antennas** | 5.8GHz, 915MHz, 433MHz | Multi-band coverage | $30-60 each |
| **RF Switch (Opera Cake)** | 4-port, USB controlled | Automated band switching | $150 |
| **LNA (Low Noise Amp)** | 0.1-6GHz, 20dB gain | Improve weak signals | $50-100 |
| **Bandpass Filters** | 2.4GHz, 5.8GHz | Reduce interference | $30-50 each |
| **GPS Module (NEO-M9N)** | I2C/USB, 10Hz | Geolocation tagging | $50-70 |
| **Cooling Fan** | 40mm, 5V | Prevent overheating | $10 |
| **Metal Case** | For HackRF/ Pi | Protection & shielding | $30-50 |

### Direction Finding (TDOA)

For drone localization, multiple HackRF units:

| Component | Quantity | Purpose |
|-----------|----------|---------|
| **HackRF One** | 2-4 units | Multi-lateration |
| **Clock Sync Cable** | 1 per unit | Synchronization |
| **GPS Disciplined Oscillator** | 1 | Precision timing |
| **Low-loss Coaxial Cables** | 4-8 | Antenna connections |

---

## 📡 Antenna Selection Guide

### Band-Specific Recommendations

| Band | Frequency | Best Antenna Type | Gain | Polarization | Beamwidth | Range |
|------|-----------|------------------|------|--------------|-----------|-------|
| **433 MHz** | 430-440 MHz | Collinear/GP | 5-8 dBi | Vertical | Omni | 2-5 km |
| **915 MHz** | 902-928 MHz | Yagi | 8-12 dBi | Linear | 60° | 3-8 km |
| **2.4 GHz** | 2.4-2.4835 GHz | Yagi/Panel | 15-20 dBi | Circular | 30-45° | 5-10 km |
| **5.8 GHz** | 5.725-5.85 GHz | Yagi/Parabolic | 15-25 dBi | Circular | 15-30° | 3-7 km |

### Antenna Types Comparison

| Type | Gain | Beamwidth | Size | Cost | Best For |
|------|------|-----------|------|------|----------|
| **Omni-directional** | 2-5 dBi | 360° | Small | $ | Portable/Mobile |
| **Yagi** | 10-20 dBi | 30-60° | Medium | $$ | Long-range fixed |
| **Patch Panel** | 15-20 dBi | 30-45° | Medium | $$ | Directional scanning |
| **Parabolic Grid** | 20-25 dBi | 15-25° | Large | $$$ | Extreme long-range |
| **Log Periodic** | 8-12 dBi | 60-90° | Medium | $$ | Multi-band coverage |

### Recommended Antenna Combos

#### Basic Setup (Single Band)
┌─────────────────────────────────────┐
│ 2.4 GHz Yagi Antenna │
│ (Covers 80% of consumer drones)│
└─────────────────────────────────────┘

text

#### Standard Setup (Dual Band)
┌─────────────────┐ ┌─────────────────┐
│ 2.4 GHz Yagi │ │ 5.8 GHz Yagi │
│ (Control Links) │ │ (Video Links) │
└─────────────────┘ └─────────────────┘

text

#### Professional Setup (Full Coverage)
┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐
│ 2.4 GHz│ │ 5.8 GHz│ │ 915 MHz│ │ 433 MHz│
│ Yagi │ │ Yagi │ │ Yagi │ │ GP │
└────────┘ └────────┘ └────────┘ └────────┘

text

---

## 🔨 Assembly Instructions

### Step 1: Prepare the SBC

#### Raspberry Pi 4 Setup
```bash
# Flash Raspberry Pi OS (64-bit) to SD card
# Download: https://www.raspberrypi.com/software/

# Enable interfaces
sudo raspi-config
# - Interface Options → SSH → Enable
# - Interface Options → SPI → Enable  
# - Interface Options → I2C → Enable

# Update system
sudo apt update && sudo apt upgrade -y

# Install SDR tools
sudo apt install -y hackrf libhackrf-dev hackrf-tools
Intel NUC Setup
bash
# Install Ubuntu 22.04 LTS
# Download: https://ubuntu.com/download

# Update system
sudo apt update && sudo apt upgrade -y

# Install dependencies
sudo apt install -y hackrf libhackrf-dev \
    libfftw3-dev libsqlite3-dev libwebsockets-dev
Step 2: Mount the HackRF One
text
Physical Mounting Options:

Option A: Stacked (Space-saving)
┌─────────────────┐
│  Raspberry Pi 4 │
├─────────────────┤
│    HackRF One   │
├─────────────────┤
│  Cooling Fan    │
└─────────────────┘
Use: 40mm M2.5 standoffs

Option B: Side-by-Side (Better cooling)
┌─────────────┐    ┌─────────────┐
│     Pi 4    │    │  HackRF One │
│             │    │             │
└─────────────┘    └─────────────┘
   10cm apart with USB cable
Step 3: Connect Antennas
text
SMA Connection Sequence:
1. Power OFF HackRF
2. Attach SMA cable to antenna
3. Connect SMA cable to HackRF ANT port  
4. Hand-tighten only (max 0.5 Nm)
5. Position antenna for optimal coverage
Step 4: USB Connection
text
IMPORTANT: Use USB 3.0 Cable and Port!

HackRF One → USB 3.0 Cable → SBC USB 3.0 Port

┌─────────────────────────────────────────┐
│ USB 3.0 required for 20 MSPS bandwidth │
│ USB 2.0 = max 10 MSPS (half speed)     │
└─────────────────────────────────────────┘
Step 5: Power Connection
text
Power Budget Calculation:

Raspberry Pi 4:       5V @ 2.5A = 12.5W
HackRF One:           5V @ 0.5A = 2.5W
Cooling Fan:          5V @ 0.2A = 1.0W
GPS Module:           3.3V @ 0.1A = 0.33W
-------------------------------------------
TOTAL:                16.33W (≈3.3A @ 5V)

Recommendation: 5V/4A (20W) power supply
Step 6: GPS Integration (Optional)
python
# I2C Connection for NEO-M9N

Raspberry Pi GPIO → GPS Module
─────────────────────────────────
Pin 1 (3.3V)    → VCC
Pin 3 (GPIO2)   → SDA (I2C Data)
Pin 5 (GPIO3)   → SCL (I2C Clock)  
Pin 6 (GND)     → GND

# Enable I2C
sudo raspi-config → Interface Options → I2C → Enable

# Test connection
sudo i2cdetect -y 1
# Should show device at 0x42
📊 Connection Diagrams
Basic Setup Diagram
text
                    ┌─────────────────┐
                    │   2.4 GHz       │
                    │   Antenna       │
                    └────────┬────────┘
                             │ SMA
                    ┌────────┴────────┐
                    │   HackRF One    │
                    │                 │
                    │  [ANT]───┐      │
                    │  [USB]───┤      │
                    └────────┬┴──────┘
                             │ USB 3.0
                    ┌────────┴────────┐
                    │ Raspberry Pi 4  │
                    │                 │
                    │ [USB3]───┐      │
                    │ [GPIO]───┤      │
                    │ [HDMI]───┘      │
                    └────────┬────────┘
                             │
                    ┌────────┴────────┐
                    │   Monitor       │
                    │  (Optional)     │
                    └─────────────────┘
Multi-Band with RF Switch
text
     ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
     │ 2.4 GHz  │ │ 5.8 GHz  │ │ 915 MHz  │ │ 433 MHz  │
     │ Antenna  │ │ Antenna  │ │ Antenna  │ │ Antenna  │
     └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘
          │            │            │            │
          └────────────┼────────────┼────────────┘
                       │            │
                  ┌────┴────┐   ┌───┴────┐
                  │ Port 1  │   │ Port 2 │
                  │ Port 3  │   │ Port 4 │
                  │ Opera   │   │        │
                  │ Cake    │   │        │
                  └────┬────┘   │        │
                       │         │        │
                  ┌────┴────┐    │        │
                  │ Common  │◄───┘        │
                  │ Port    │             │
                  └────┬────┘             │
                       │                  │
                  ┌────┴────┐             │
                  │ HackRF  │             │
                  │  ANT    │             │
                  └─────────┘             │
                       │                  │
                  ┌────┴────┐             │
                  │  USB    │             │
                  │ Control │─────────────┘
                  └─────────┘      (GPIO)
TDOA Direction Finding (Dual HackRF)
text
┌─────────────────────────────────────────────────────────┐
│                 TDOA Direction Finding                   │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  ┌─────────┐         ┌─────────┐        ┌─────────┐    │
│  │ Antenna │         │ Antenna │        │ Antenna │    │
│  │   #1    │         │   #2    │        │   #3    │    │
│  └────┬────┘         └────┬────┘        └────┬────┘    │
│       │                   │                  │          │
│  ┌────┴────┐          ┌───┴───┐          ┌───┴───┐    │
│  │HackRF #1│          │HackRF#2│          │HackRF#3│    │
│  └────┬────┘          └───┬───┘          └───┬───┘    │
│       │                   │                  │          │
│       └─────────┬─────────┼──────────────────┘          │
│                 │         │                             │
│            ┌────┴─────┐   │                             │
│            │ PPS Sync │   │                             │
│            │ (GPSDO)  │   │                             │
│            └────┬─────┘   │                             │
│                 │         │                             │
│            ┌────┴─────┐   │                             │
│            │  USB Hub │   │                             │
│            └────┬─────┘   │                             │
│                 │         │                             │
│            ┌────┴─────┐   │                             │
│            │   SBC    │◄──┘                             │
│            └──────────┘                                 │
└─────────────────────────────────────────────────────────┘
⚡ Power Requirements
Power Supply Specifications
Component	Voltage	Current	Connector	Regulation
Raspberry Pi 4	5V DC	3A (min)	USB-C	±5%
HackRF One	5V DC	500mA	USB Micro	±10%
Opera Cake	5V DC	100mA	USB Mini	±5%
GPS Module	3.3/5V	50mA	Pin header	±5%
Cooling Fan	5V DC	200mA	2-pin	±10%
Power Supply Recommendations
text
Basic Setup (Pi + HackRF):
┌─────────────────────────────────────┐
│  USB-C Power Supply                 │
│  5V / 3.5A (17.5W)                 │
│  Recommended: Official Pi 4 PSU    │
└─────────────────────────────────────┘

Full Setup (With extras):
┌─────────────────────────────────────┐
│  Powered USB Hub                    │
│  5V / 4A (20W)                      │
│  + Individual device power          │
└─────────────────────────────────────┘

Portable Setup (Field use):
┌─────────────────────────────────────┐
│  Power Bank                         │
│  5V / 4A (20W)                      │
│  Capacity: 20,000mAh+               │
│  Runtime: 4-6 hours                 │
└─────────────────────────────────────┘
Power Consumption by Mode
Mode	Pi 4	HackRF	Total	Battery (20Ah)
Idle	3W	0.5W	3.5W	28 hours
Scanning	5W	1.5W	6.5W	15 hours
Active Detection	8W	2.5W	10.5W	9.5 hours
Full Load	12W	2.5W	14.5W	7 hours
📍 Mounting & Placement
Environmental Requirements
Parameter	Min	Recommended	Max
Temperature	0°C	25°C	50°C
Humidity	10%	50%	80% (non-condensing)
RF Noise Floor	-110dBm	-100dBm	-80dBm
Line of Sight	0%	50%	100% to target
Antenna Placement Guide
text
Optimal Placement (Roof/Mast):
┌─────────────────────────────┐
│          Antennas           │
│         (2-5m high)         │
│              │              │
│         ┌────┴────┐         │
│         │   Mast  │         │
│         │   2-5m  │         │
│         └────┬────┘         │
│              │              │
│    ┌─────────┴─────────┐    │
│    │   HackRF + Pi     │    │
│    │   (Weatherproof   │    │
│    │    enclosure)     │    │
│    └───────────────────┘    │
└─────────────────────────────┘

Ground Level Placement:
┌─────────────────────────────┐
│   Antennas on Tripod        │
│   (1.5-2m height)           │
│         │                    │
│    ┌────┴────┐               │
│    │  Table  │               │
│    │  Setup  │               │
│    └─────────┘               │
└─────────────────────────────┘
Avoid Interference Sources
Source	Distance Needed	Mitigation
WiFi Routers	>10m	Use 5GHz band
Microwave Ovens	>20m	Shielding
Cell Towers	>50m	Bandpass filters
High-voltage lines	>30m	Keep away
Metal objects	>1m	Reposition
🎯 Calibration Procedure
Frequency Calibration
bash
# 1. Set HackRF to known frequency
hackrf_transfer -f 2450000000 -s 2000000

# 2. Measure with spectrum analyzer or known source
# 3. Calculate offset (PPM)

# 4. Apply correction
hackrf_set_freq_correction <ppm_value>

# Example for 2.4 GHz (typically 0.5-2 ppm)
hackrf_set_freq_correction 1.5
Gain Calibration
bash
# Automatic gain optimization
python3 calibrate_gain.py --band 2.4 --sweep

# Manual gain setting
hackrf_set_lna_gain 32    # 0-40 dB
hackrf_set_vga_gain 20    # 0-62 dB
Noise Floor Measurement
bash
# Measure noise floor
hackrf_sweep -f 2400000000:2483500000 -w 1000000 -N 10

# Expected values:
# Rural: -105 to -110 dBm
# Suburban: -95 to -105 dBm
# Urban: -85 to -95 dBm
# Industrial: -75 to -85 dBm
🐛 Troubleshooting Hardware
HackRF Not Detected
Symptom	Cause	Solution
hackrf_info shows no device	Driver issue	Install WinUSB (Windows) / udev rules (Linux)
Device found but no RX	USB cable	Use USB 3.0 cable
Intermittent connection	Power	Use powered USB hub
Overheating	Cooling	Add fan, reduce gain
Poor Reception
Symptom	Cause	Solution
Weak signals	Antenna gain	Upgrade to higher gain antenna
High noise floor	Interference	Use bandpass filters
No signals	Connection	Check SMA cables
Distorted signals	Overload	Reduce LNA gain
Commands for Diagnosis
bash
# Check device
hackrf_info
lsusb | grep HackRF

# Test RX
hackrf_sweep -f 2400000000:2483500000 -w 1000000

# Check temperature
hackrf_debug | grep temp

# Monitor USB bandwidth
sudo cat /sys/kernel/debug/usb/devices | grep -A 10 HackRF
🔧 Maintenance
Daily Checks
Verif y HackRF detected (hackrf_info)

Check antenna connections

Monitor noise floor

Verify cooling fan operation

Weekly Maintenance
Clean antenna connectors

Check SMA cable integrity

Review system logs

Backup database

Monthly Maintenance
Update firmware

Recalibrate frequency

Inspect for corrosion

Test with known signal source

Firmware Update
bash
# Download latest firmware
git clone https://github.com/greatscottgadgets/hackrf.git
cd hackrf/firmware

# Update
hackrf_spiflash -w hackrf_one_usb.bin

# Verify
hackrf_info
🚀 Advanced Configurations
Weatherproof Enclosure
text
For Outdoor Installation:

┌─────────────────────────────────────┐
│  IP65/NEMA 4 Enclosure              │
│  ┌─────────────────────────────┐   │
│  │  Desiccant packs             │   │
│  │  ┌─────────┐  ┌─────────┐  │   │
│  │  │    Pi   │  │ HackRF  │  │   │
│  │  └─────────┘  └─────────┘  │   │
│  │  ┌─────────────────────┐    │   │
│  │  │    Cooling Fan      │    │   │
│  │  │    (Air circulation)│    │   │
│  │  └─────────────────────┘    │   │
│  └─────────────────────────────┘   │
│         │         │                 │
│    SMA Bulkhead  USB/Ethernet      │
│    Connectors    Gland              │
└─────────────────────────────────────┘
Solar Powered Setup
text
┌─────────────┐     ┌─────────────┐
│ Solar Panel │     │ Battery     │
│ 50-100W     │────▶│ 12V 50Ah    │
└─────────────┘     └──────┬──────┘
                           │
                      ┌────┴────┐
                      │ 12V-5V  │
                      │ DC-DC   │
                      └────┬────┘
                           │
                    ┌──────┴──────┐
                    │ Pi + HackRF │
                    └─────────────┘

Runtime: 24/7 in sunny climates
Battery backup: 3-5 days without sun
Multiple Unit Synchronization
bash
# Master HackRF
hackrf_clock -e      # Enable clock output

# Slave HackRF(s)
hackrf_clock -i      # Use external clock input

# Verify sync
hackrf_sweep -f 2400000000 -t 1000000
📊 Performance Expectations
Range by Drone Type
Drone Type	2.4 GHz Range	5.8 GHz Range	Notes
DJI Mini	500m	300m	Limited power
DJI Mavic	1500m	800m	Standard
DJI Phantom	2000m	1000m	Higher power
FPV Racing	1000m	600m	Directional
Military	5000m+	3000m+	Encrypted
Detection Probability
Condition	Probability	Notes
Clear LOS, <500m	95%	Optimal
Clear LOS, 500-1000m	80%	Good
Partial obstacles, <500m	60%	Fair
Urban, <500m	40%	Reduced
Heavy RF noise	25%	Poor
