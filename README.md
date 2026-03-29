# 🏎️ E116 Autonomous Race Car — Lab Week 1

![Lab Setup Banner](Lehigh_Lab1.jpg)
<!-- Replace: wide shot of the car + monitor on the lab bench -->

---

## 📋 Table of Contents

- [Overview](#overview)
- [Part 1 — Hardware](#part-1--hardware)
  - [1.1 Lab Environment Setup](#11-lab-environment-setup)
  - [1.2 Car Components](#12-car-components)
  - [1.3 Component Deep Dive](#13-component-deep-dive)
  - [1.4 Power Test](#14-power-test)
- [Part 2 — Software](#part-2--software)
  - [2.1 Ubuntu Basics](#21-ubuntu-basics)
  - [2.2 Linux Commands](#22-linux-commands)
  - [2.3 Text Editors](#23-text-editors)
- [Carrier Board Reference](#carrier-board-reference)
- [Safety Rules](#safety-rules)
- [Repository Structure](#repository-structure)

---

## Overview

The **E116** is a 1/16-scale autonomous race car built on a Traxxas E-Revo chassis with an NVIDIA Jetson Orin Nano for GPU-accelerated edge compute, an Intel RealSense stereo camera for depth perception, and a custom carrier board handling power management, sensor interfaces, and drive-train control.

This guide walks through hardware identification, voltage measurements, booting the Jetson into Ubuntu, and basic Linux terminal operations.

---

## Part 1 — Hardware

### 1.1 Lab Environment Setup

![DMM Setup](.jpg)
<!-- Replace: photo of the Fluke 8800A or GwInstek DMM with probes connected -->

1. Locate the **120 V AC outlet** on the bench.
2. Plug in the AC-DC power converter, then disconnect the converter from the cord (leave the cord in the wall).
3. Find the **Digital Multimeter** (Fluke 8800A or GwInstek GDM-8245). Insert the red and black probes into the top-left socket. Power on the DMM.

#### AC Measurement

4. Press **AC V** on the DMM.
5. Measure the open power cord voltage. Record the value.

![AC Voltage Measurement](assets/images/ac_measurement.jpg)
<!-- Replace: photo of DMM probes on the AC power cord -->

#### DC Measurement

6. Reconnect the converter to the power cord.
7. Press **DC V** on the DMM.
8. Measure the barrel connector output voltage. Compare against the converter label.

![DC Voltage Measurement](assets/images/dc_measurement.jpg)
<!-- Replace: photo of DMM probes on the barrel connector output -->

---

### 1.2 Car Components

| Component | Model | Est. Price | Notes |
|-----------|-------|------------|-------|
| Traxxas 1/16 Car | 1/16 E-Revo VXL TSM | $ ___ | AWD chassis, Ackerman steering |
| Brushless Motor | Velineon® 380 | $ ___ | No contact brushes, higher efficiency |
| RC Handheld | TQi 2.4 GHz TSM | $ ___ | Manual override control |
| Dual Battery Charger | EZ-Peak 8A 3S | $ ___ | Traxxas |
| LiPo Battery Charger | X1, 200 W | $ ___ | OVONIC |
| LiPo Battery | OVONIC | $ ___ | High energy density, rechargeable |
| NiMH Battery | Traxxas | $ ___ | Lower density than LiPo |
| Stereo Camera | Intel RealSense D435 | $ ___ | Depth + RGB stereo vision |
| Jetson Dev Kit | Orin Nano 8 GB | $ ___ | NVIDIA GPU edge compute |
| Carrier Board | LU v2.1 | ~$105 | Power mgmt, sensor I/F, drive-train ctrl |

![Car Components Annotated](assets/images/car_components_annotated.jpg)
<!-- Replace: annotated top-down photo of the car with arrows to each component -->

---

### 1.3 Component Deep Dive

1. Pick **3 components** from the table. Research their specs, unique features, and market competitors.
2. The full-scale E116 platform uses a **LiDAR sensor** (instead of stereo camera) and a **VESC** (instead of the stock Traxxas ESC). Consider how these alternatives compare in cost, accuracy, and integration complexity.

![Component Comparison](assets/images/component_comparison.jpg)
<!-- Replace: side-by-side photo or diagram comparing sensor/ESC alternatives -->

---

### 1.4 Power Test

![Car Powered On — NVIDIA Boot Screen](assets/images/car_powered_on.jpg)
<!-- Replace with your photo (e.g. Lehigh_Lab1.jpg) showing the car next to the NVIDIA splash -->

**Procedure:**

1. Inspect the car for loose screws, wires, or connections. Fix anything out of place.
2. Connect **monitor** (DisplayPort), **keyboard**, and **mouse** to the Orin Nano.
3. Plug the AC-DC converter into the **Main Barrel** on the carrier board → Main LED turns on.
4. Press the **Jetson Power** button. Flip the **Drive-train Power Switch**. Verify:
   - Status LEDs 1–3 are lit
   - Green light on the Orin Nano
   - Fan is spinning
5. Power on the **RC handheld** near the car. Confirm:
   - RC receiver LED turns **green**
   - Status LED 4 turns on
6. Turn off RC power.
7. Wait ~2 minutes. Switch the monitor input to **DisplayPort**.
8. You should see the NVIDIA logo, then the Ubuntu login screen.

<!-- VIDEO: Boot sequence from power button press to Ubuntu login -->
https://github.com/user-attachments/assets/VIDEO_ID_HERE
<!-- Replace: upload a short video of the boot sequence and paste the GitHub video link -->

> ⛔ **Safety** — Always place the car on a solid stand during power tests. Wheels will spin. Turn off power before disconnecting anything. Match red (+) to positive, black to GND.

---

## Part 2 — Software

### 2.1 Ubuntu Basics

#### Login Credentials

Replace `XX` with your car number:

| | Username | Password |
|---|----------|----------|
| **Monday** | `team1XX` | `robot1XXPA##!` |
| **Wednesday** | `team3XX` | `robot3XXPA##@` |

#### Wi-Fi Networks

| Network | Password | Room |
|---------|----------|------|
| `PinkPig` | `GetLost2022` | PA 331 |
| `ECE_Lab` | `ECElab332` | PA 332 |

**Steps:**

1. Log in to Ubuntu with the credentials above.
2. Verify Wi-Fi connectivity. Open Firefox.
3. Open Files → navigate to `~/Documents` → create a new subfolder → move `game.py` into it.
4. Open **Software & Updates** → Updates tab → set "Automatically check for updates" to **Never**.
5. Open a **Terminal** and pin it to the Favorites bar.

![Ubuntu Desktop](assets/images/ubuntu_desktop.jpg)
<!-- Replace: screenshot of the Ubuntu desktop with Terminal pinned -->

---

### 2.2 Linux Commands

#### Command Reference

| Command | Description |
|---------|-------------|
| `ls -al` | List all files with permissions and hidden entries |
| `cd folder_name` | Change into a directory |
| `cd ..` | Go up one level |
| `cd ~` | Go to home directory |
| `mkdir name` | Create a new directory |
| `cp f1 f2` | Copy a file |
| `mv src dest` | Move or rename a file |
| `rm -r dir` | Remove a directory recursively |
| `grep pattern file` | Search for a pattern in a file |
| `chmod a+rwx file` | Give all users read/write/execute |
| `chmod 777 file` | Same as above (numeric form) |

#### Terminal Shortcuts

| Shortcut | Action |
|----------|--------|
| `Tab` | Auto-complete file/folder names |
| `Ctrl+C` | Kill running process |
| `Ctrl+Z` | Suspend process |
| `Ctrl+D` | Exit the shell |

#### Exercise

```bash
# Navigate to your subfolder
cd ~/Documents/your_subfolder

# Check file permissions
ls -l game.py

# Make it executable
chmod a+x game.py

# Run it
python3 game.py
```

![Terminal Commands](assets/images/terminal_commands.jpg)
<!-- Replace: screenshot showing ls -l output and chmod in the terminal -->

**Further reading:**
- [Ubuntu CLI Tutorial (parts 4–6)](https://ubuntu.com/tutorials/command-line-for-beginners)
- [linuxcommand.org](http://linuxcommand.org)
- [Unix Quick Reference Card (PDF)](https://files.fosswire.com/2007/08/fwunixref.pdf)

---

### 2.3 Text Editors

Pick an editor and create `compute.py`:

```bash
gedit compute.py    # GUI editor — easiest
nano compute.py     # Terminal-based, beginner-friendly
vim compute.py      # Powerful, steep learning curve
```

Type the following:

```python
# simple computation by python
a = 10
b = 5
c = a * b
print("c = " + str(c))
```

Save, close, and run:

```bash
python3 compute.py
# Expected output: c = 50
```

![Text Editor](assets/images/text_editor.jpg)
<!-- Replace: screenshot of your editor with compute.py open -->

<!-- VIDEO: Screen recording of writing, saving, and running compute.py -->
https://github.com/user-attachments/assets/VIDEO_ID_HERE
<!-- Replace: upload a screen recording and paste the GitHub video link -->

---

## Carrier Board Reference

The **E116 carrier board (LU v2.1)** sits between the Jetson and the Traxxas chassis, providing power management, sensor interfacing, and drive-train control.

![Carrier Board Functional Blocks](assets/images/carrier_board_diagram.jpg)
<!-- Replace: annotated photo or block diagram of the carrier board -->

| Block | Description |
|-------|-------------|
| Main Power | Barrel connector input, voltage regulation, battery checker |
| Jetson Signal Interface | Routes GPIO, I2C, UART to the Orin Nano header |
| Drive Control | PWM outputs for motor ESC and steering servo |
| Sensing & Control | Sensor connectors, external IMU interface |
| Comm Ports | I2C and UART breakout headers |
| Status LEDs 1–4 | Power, drive-train, and RC link indicators |
| Mode Switch | Operating mode selector |
| 0.92″ OLED Screen | On-board status display |

---

## Safety Rules

### ⛔ Critical

- **DO NOT** stand on stools
- **DO NOT** point sharp tools at people
- **DO NOT** drop metal objects on powered circuits
- Keep the car on a **solid stand** when wheels might spin
- **Turn off power** before disconnecting any components
- Match polarity: 🔴 **red = V+** · ⚫ **black = GND**
- **No food or drink** in the lab

### 💡 Best Practices

- Unplug batteries and turn off RC handheld when leaving — draining damages LiPo cells
- Check charge levels; rubber-band a battery once fully charged
- Hold **connectors** (not wires) when unplugging cables
- Tidy the bench and collect all tools before leaving
- Log out from lab computers

---

## Repository Structure

```
.
├── README.md
├── assets/
│   ├── images/
│   │   ├── lab_setup_banner.jpg
│   │   ├── dmm_setup.jpg
│   │   ├── ac_measurement.jpg
│   │   ├── dc_measurement.jpg
│   │   ├── car_components_annotated.jpg
│   │   ├── component_comparison.jpg
│   │   ├── car_powered_on.jpg
│   │   ├── ubuntu_desktop.jpg
│   │   ├── terminal_commands.jpg
│   │   ├── text_editor.jpg
│   │   └── carrier_board_diagram.jpg
│   └── videos/
│       ├── boot_sequence.mp4
│       └── compute_py_demo.mp4
└── src/
    ├── game.py
    └── compute.py
```