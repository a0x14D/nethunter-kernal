# Kali NetHunter Kernel for Miatoll (crDroid / Android 17 Edition)

> **Custom Kali NetHunter kernel for Xiaomi Miatoll devices (Redmi Note 9 Pro Max, Note 9 Pro, Note 9S, POCO M2 Pro) running crDroid / Android 17 with internal monitor mode, packet injection, USB Wi-Fi, SDR, CAN Bus, and hardware hacking support.**

Built from the **OpenELA / Stormbreaker** Linux 4.14 (`4.14.357`) source tree, specifically optimized for **crDroid (Android 17 / 14)** on the **Qualcomm Snapdragon 720G (SM6250)** platform.

---

## 📱 Supported Devices (`miatoll`)

This kernel utilizes a universal AnyKernel3 installer supporting all devices on the Snapdragon 720G platform:

| Device Codename | Commercial Name | Model |
| --------------- | --------------- | ----- |
| `excalibur`     | Redmi Note 9 Pro Max | Global / India |
| `curtana`       | Redmi Note 9S / Redmi Note 9 Pro (India) | Global / India |
| `joyeuse`       | Redmi Note 9 Pro (Global with NFC) | Global |
| `gram`          | POCO M2 Pro | India |

---

## ⚡ Features & Capabilities

### 📡 1. Wireless Penetration Testing
- **Internal Qualcomm Wi-Fi (`wlan0` - WCN3990 via `qcacld-3.0`):**
  - **Monitor Mode (`wlan_hdd_rx_monitor`):** Full raw 802.11 frame capture directly on the phone's internal antenna without external hardware.
  - **Packet Injection (`wlan_hdd_frame_inject`):** Custom WMA frame injection queue, sequence number preservation, and QoS header preservation.
  - Fully compatible with `airmon-ng`, `airodump-ng`, `aireplay-ng`, and `wifite`.
- **External USB Wi-Fi Adapters (`mac80211` Stack):**
  - **Atheros AR9271 (`ath9k_htc.ko`):** Alfa AWUS036NHA, TP-Link TL-WN722N v1 (injection & monitor mode).
  - **Atheros AR9170 (`carl9170.ko`):** Dual-band 802.11n USB adapters.
  - **Ralink RT3070 / RT5370 (`rt2800usb.ko`):** Alfa AWUS036NEH, Panda Wireless PAU05/PAU09.
  - **Realtek RTL8187L (`rtl8187.ko`):** Classic Alfa AWUS036H.
  - **Realtek RTL8188EUS / RTL8192EU (`rtl8xxxu.ko`):** Compact nano adapters.
  - Wireless Extensions (`CONFIG_CFG80211_WEXT=y`) enabled for legacy tool compatibility.

### 🔌 2. Hardware Hacking, IoT & Reverse Engineering (USB Serial)
- Plug-and-play USB OTG access to hardware security tools:
  - **FTDI (`ftdi_sio.ko`):** FT232R, FT2232D (Bus Pirate, Tigard, JTAGulator, hardware analyzers).
  - **Silicon Labs (`cp210x.ko`):** CP2102/CP2104 (ESP32, ESP8266, NodeMCU, smart device UART consoles).
  - **WCH (`ch341.ko`):** CH340G, CH341A (EEPROM/BIOS flashers, DIY development boards).
  - **Prolific (`pl2303.ko`):** Network switch and router console cables.
  - **USB CDC ACM (`cdc-acm.ko`):** Flipper Zero CLI, Proxmark3 (RFID/NFC), Teensy, Arduino.
- Direct interactive access via NetHunter terminal using `picocom`, `minicom`, or `screen /dev/ttyUSB0`.

### 📻 3. Software Defined Radio (SDR) & RF Security
- `dvb-usb-rtl28xxu.ko` & `rtl2832.ko`, `rtl2832_sdr.ko`: RTL-SDR USB dongle support.
- Tuner modules included: `r820t.ko`, `e4000.ko`, `fc0012.ko`, `fc0013.ko`, `fc2580.ko`, `si2157.ko`, `qt1010.ko`.
- Run `rtl_433` (sniffing 433 MHz/315 MHz wireless sensors, weather stations, garage door openers, TPMS tire pressure sensors), `rtl_sdr`, and `gqrx` directly from mobile.

### 🚗 4. Automotive Security (SocketCAN / Car Hacking)
- Full SocketCAN kernel networking subsystem (`CONFIG_CAN=y`, `CONFIG_CAN_RAW=y`, `CONFIG_CAN_BCM=y`, `CONFIG_CAN_GW=y`).
- **Virtual CAN (`CONFIG_CAN_VCAN=y`):** Create `vcan0` for running ICSim and practicing vehicle CAN reverse-engineering without a physical car.
- **Serial CAN (`slcan.ko`):** Connect CANable (candleLight / slcan firmware) or USB OBD-II bridges.
- Compatible with `candump`, `cansniffer`, `canplayer`, and `cangen`.

### 🛡️ 5. Traffic Redirection, Transparent Proxying & MITM
- `CONFIG_NETFILTER_XT_TARGET_REDIRECT=y`: Redirect port 80/443 traffic locally for **bettercap**, **mitmproxy**, or **Burp Suite**.
- `CONFIG_NETFILTER_XT_TARGET_TPROXY=y`: Non-NAT transparent proxying.
- `CONFIG_BRIDGE_NETFILTER=y`: Layer 2 Ethernet bridge sniffing and frame inspection.
- `CONFIG_IP_ADVANCED_ROUTER=y` & `CONFIG_IP_MULTIPLE_TABLES=y`: Multi-interface policy routing.
- `CONFIG_NETFILTER_NETLINK_QUEUE=y`: NFQUEUE packet interception for Scapy / Python packet inspection.

### 💻 6. BadUSB & USB Gadget Emulation
- `CONFIG_USB_CONFIGFS_F_HID=y`: DuckHunter / Rubber Ducky HID keyboard and mouse injection via the Kali NetHunter app.
- `CONFIG_USB_CONFIGFS_MASS_STORAGE=y`: DriveDroid raw bootable ISO image emulation.
- `CONFIG_USB_CONFIGFS_RNDIS=y` & `CONFIG_USB_CONFIGFS_ECM=y`: USB Ethernet emulation for PoisonTap and Responder credential capture.

### 🔍 7. Forensics & Firmware Analysis Filesystems
- `CONFIG_SQUASHFS=y` (with XZ, ZLIB, LZ4 decompression): Directly mount and inspect router/camera SquashFS firmwares unpacked with `binwalk`.
- `CONFIG_ISO9660_FS=y`: Mount raw CD/DVD filesystem images.
- `udf.ko`: Universal Disk Format support.
- `CONFIG_FUSE_FS=y`: Supports `sshfs`, `encfs`, `veracrypt`, and userspace filesystem tools.

### 🌐 8. USB/IP (Remote USB Device Redirection)
- `usbip-core.ko`, `usbip-host.ko`, `vhci-hcd.ko`: Forward physical USB peripherals attached to the phone over Wi-Fi/VPN to a desktop Kali workstation, or vice versa.

### 🤖 9. Android 17 / crDroid Compatibility Fixes
- **No DTBO Overwrite:** `dtbo.img` is intentionally omitted from the AnyKernel3 flasher to protect the ROM's device tree overlay (prevents bootloops and camera/Wi-Fi breakage on crDroid / Android 17).
- **Clean Kernel Release:** Clean `4.14.357-openela-Stormbreaker-NetHunter-miatoll` naming without SHA1 hash suffixes, guaranteeing module autoloading from `/lib/modules/$(uname -r)/`.
- **SELinux Permissive Capability:** `CONFIG_SECURITY_SELINUX_DEVELOP=y` allows switching to permissive mode (`setenforce 0`) for root NetHunter raw socket operations.

---

## 📦 What's Included in the Release Zip

The release zip (`anykernel-nethunter-miatoll-20261124-135144.zip`) contains:

```
├── anykernel.sh                                              # AnyKernel3 installer script
├── banner                                                    # NetHunter ASCII installation banner
├── Changelog.txt                                             # Build commit history
├── Image.gz-dtb                                              # 17.5 MB compiled kernel image + DTB
├── META-INF/                                                 # Recovery flashing scripts & binaries
├── modules/                                                  # Kernel modules (.ko) installed to /system_root/lib/modules/
│   └── system_root/lib/modules/4.14.357-openela-Stormbreaker-NetHunter-miatoll/
│       ├── kernel/drivers/media/usb/dvb-usb-v2/dvb-usb-rtl28xxu.ko
│       ├── kernel/drivers/media/dvb-frontends/rtl2832.ko
│       ├── kernel/drivers/net/can/slcan.ko
│       ├── kernel/drivers/net/wireless/ath/ath9k/ath9k_htc.ko
│       ├── kernel/drivers/net/wireless/ralink/rt2x00/rt2800usb.ko
│       ├── kernel/drivers/net/wireless/realtek/rtl818x/rtl8187/rtl8187.ko
│       ├── kernel/drivers/net/wireless/realtek/rtl8xxxu/rtl8xxxu.ko
│       ├── kernel/drivers/usb/serial/ftdi_sio.ko
│       ├── kernel/drivers/usb/serial/cp210x.ko
│       ├── kernel/drivers/usb/serial/ch341.ko
│       ├── kernel/drivers/usb/serial/pl2303.ko
│       ├── kernel/drivers/usb/class/cdc-acm.ko
│       ├── kernel/drivers/usb/usbip/usbip-core.ko
│       └── kernel/techpack/data/drivers/rmnet/...
└── tools/                                                    # magiskboot, busybox, ak3-core.sh
```

---

## 📝 Changelog

### Version 2.0 (2026-11-24) — crDroid Android 17 / Full Cyber Research Edition
- **Fixed:** Resolved `Image.gz-dtb` generation and toolchain path issues with Android Clang 10.0 and Google GCC 4.9.
- **Fixed:** Added OpenSSL 4.1.0 compatibility guards for host tools (`extract-cert.c` and `sign-file.c`).
- **Fixed:** Corrected `LINUX_COMPILER` macro evaluation in `scripts/mkcompile_h`.
- **Added:** Integrated `qcacld-3.0` packet injection and monitor mode framework (`wlan_hdd_frame_inject`).
- **Added:** Enabled WCN3990 monitor mode handling in `wlan_hdd_rx_monitor.c` and `wlan_hdd_rx_monitor.h`.
- **Added:** External USB Wi-Fi drivers (`ath9k_htc`, `carl9170`, `rt2800usb`, `rtl8187`, `rtl8xxxu`).
- **Added:** Hardware hacking USB serial drivers (FTDI, CP210x, CH341, PL2303, CDC ACM).
- **Added:** Software Defined Radio support (RTL-SDR `rtl28xxu` + full tuner stack).
- **Added:** Automotive SocketCAN subsystem, `vcan0` virtual CAN, and `slcan`.
- **Added:** MITM transparent proxying (`REDIRECT`, `TPROXY`, bridge netfilter, NFQUEUE).
- **Added:** Forensics filesystems (SquashFS multi-decompression, ISO9660, UDF).
- **Added:** USB/IP peripheral redirection modules.
- **Improved:** Prevented `dtbo.img` overwrite to maintain crDroid / Android 17 display, camera, and Wi-Fi stability.
- **Improved:** Resolved circular module symlinks during packaging.

---

## 📋 Installation Instructions

1. **Prerequisites:**
   - Redmi Note 9 Pro Max / 9S / 9 Pro / POCO M2 Pro (`miatoll`)
   - Unlocked bootloader
   - Custom Recovery installed (**OrangeFox** or **TWRP**)
   - crDroid / Android 17 or any AOSP/LineageOS custom ROM installed
   - **Full Nandroid backup** taken in recovery before flashing

2. **Flashing:**
   - Transfer `anykernel-nethunter-miatoll-20261124-135144.zip` to your internal storage or SD card.
   - Reboot to Recovery (Power + Volume Up).
   - Select **Install** -> Choose `anykernel-nethunter-miatoll-20261124-135144.zip`.
   - Swipe to confirm flash.
   - (Optional) Wipe Dalvik & Cache.
   - Reboot System.

---

## 🧪 Testing in Kali NetHunter Terminal

Open the Kali NetHunter Terminal (`nh` or chroot) and verify your features:

### 1. Internal Wi-Fi Monitor Mode (`wlan0`)
```bash
# Check interface status
ip link show wlan0

# Put wlan0 into monitor mode
airmon-ng start wlan0
# or:
iw dev wlan0 interface add mon0 type monitor
ip link set up dev mon0

# Verify monitor interface
iwconfig

# Test packet capture
airodump-ng mon0

# Test packet injection
aireplay-ng --test mon0
```

### 2. External USB Wi-Fi Adapter
```bash
# Plug in your Alfa or Panda adapter via OTG
lsusb
dmesg | tail -n 20

# Interface should appear as wlan1
ip link show wlan1
airmon-ng start wlan1
```

### 3. Virtual CAN Bus (Car Hacking)
```bash
# Bring up virtual CAN bus
ip link add dev vcan0 type vcan
ip link set up vcan0

# Verify interface
ip link show vcan0

# Listen on the CAN bus
candump vcan0
```

### 4. USB Serial & Hardware Hacking
```bash
# Connect Flipper Zero, Proxmark3, or ESP32 via OTG
ls -la /dev/ttyUSB* /dev/ttyACM*

# Connect to serial console
picocom -b 115200 /dev/ttyUSB0
```

### 5. Check Loaded Modules
```bash
lsmod
```

---

## 🤝 Credits & Acknowledgements

- **Kali NetHunter Team** & Re4son for the NetHunter project.
- **osm0sis** for **AnyKernel3**.
- **OpenELA & Stormbreaker Developers** for the robust 4.14 kernel source.
- **kimocoder**, **Loukious**, and **Cyber Knight** for the `qcacld-3.0` packet injection patches.
- Xiaomi / Miatoll kernel contributors and community testers.
