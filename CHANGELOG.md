# Kali NetHunter Kernel Changelog for Miatoll (crDroid 17)

## [v2.0-crDroid-17] - 2026-11-24

### 📦 Release Artifact
- **File:** `anykernel-nethunter-miatoll-20261124-135144.zip`
- **Kernel Release:** `4.14.357-openela-Stormbreaker-NetHunter-miatoll`
- **Target OS:** crDroid Android 17 / 14 (AOSP / LineageOS)
- **Target Platform:** Qualcomm Snapdragon 720G (`miatoll` - excalibur, curtana, joyeuse, gram)

### 🚀 Highlights & Features Added
- **Internal Wi-Fi Monitor Mode & Packet Injection:**
  - Integrated `qcacld-3.0` packet injection patch with WMA injection queue and QoS preservation
  - Enabled WCN3990 monitor mode handling in `wlan_hdd_rx_monitor.c` and `wlan_hdd_rx_monitor.h`
  - Tested and confirmed working in Kali NetHunter terminal with `airmon-ng` and `airodump-ng`
- **External USB Wi-Fi Drivers (`mac80211`):**
  - Added `ath9k_htc.ko` (Alfa AWUS036NHA / TP-Link TL-WN722N v1)
  - Added `carl9170.ko` (Atheros AR9170 dual-band)
  - Added `rt2800usb.ko` (Alfa AWUS036NEH / Panda Wireless)
  - Added `rtl8187.ko` (Alfa AWUS036H)
  - Added `rtl8xxxu.ko` (Realtek RTL8188EUS / RTL8192EU)
- **Hardware Hacking & IoT / USB-to-UART:**
  - Added `ftdi_sio.ko` (FTDI FT232R / FT2232D for Bus Pirate, Tigard, JTAGulator)
  - Added `cp210x.ko` (Silicon Labs CP2102/4 for ESP32 / NodeMCU / IoT debugging)
  - Added `ch341.ko` (WCH CH340 / CH341A EEPROM flashers and dev boards)
  - Added `pl2303.ko` (Prolific USB-to-Serial console adapters)
  - Added `cdc-acm.ko` (Flipper Zero CLI, Proxmark3 RFID/NFC, Teensy, Arduino)
- **Software Defined Radio (SDR) & RF Security:**
  - Added `dvb-usb-rtl28xxu.ko` (RTL-SDR USB dongle support)
  - Added `rtl2832.ko`, `rtl2832_sdr.ko`, and RF tuners (`r820t.ko`, `e4000.ko`, `fc0012.ko`, `fc0013.ko`, `fc2580.ko`, `si2157.ko`, `qt1010.ko`)
- **Automotive CAN Bus Security:**
  - Added SocketCAN network stack (`CONFIG_CAN=y`, `CONFIG_CAN_RAW=y`, `CONFIG_CAN_BCM=y`)
  - Added `CONFIG_CAN_VCAN=y` for virtual CAN testing (`vcan0`) without physical vehicle
  - Added `slcan.ko` for CANable and OBD-II serial bridges
- **MITM & Network Redirection:**
  - Enabled `CONFIG_NETFILTER_XT_TARGET_REDIRECT=y` for transparent proxying (bettercap / mitmproxy)
  - Enabled `CONFIG_NETFILTER_XT_TARGET_TPROXY=y`
  - Enabled `CONFIG_BRIDGE_NETFILTER=y` for Layer 2 frame filtering
  - Enabled `CONFIG_NETFILTER_NETLINK_QUEUE=y` (NFQUEUE for Scapy/Python interception)
- **BadUSB & USB Gadget Emulation:**
  - `CONFIG_USB_CONFIGFS_F_HID=y` (DuckHunter / HID keystroke injection)
  - `CONFIG_USB_CONFIGFS_MASS_STORAGE=y` (DriveDroid bootable ISO emulation)
  - `CONFIG_USB_CONFIGFS_RNDIS=y` & `CONFIG_USB_CONFIGFS_ECM=y` (USB Ethernet credential harvesting)
- **Forensics & Firmware Analysis:**
  - `CONFIG_SQUASHFS=y` with XZ/ZLIB/LZ4 for mounting extracted router/IoT firmwares
  - `CONFIG_ISO9660_FS=y` for disk image mounting
  - `udf.ko` for Universal Disk Format images
- **USB/IP:**
  - Added `usbip-core.ko`, `usbip-host.ko`, `vhci-hcd.ko` for network USB forwarding
- **Android 17 / crDroid Fixes:**
  - Omitted `dtbo.img` from flasher to avoid overwriting ROM device tree and causing bootloops
  - Fixed kernel release string to match module directories without git SHA1 hash mismatches
  - Enabled `CONFIG_SECURITY_SELINUX_DEVELOP=y` for permissive mode support

---

## [v1.0] - 2026-11-14
- Initial Kali NetHunter kernel build based on OpenELA / Stormbreaker Linux 4.14.357 tree.
- Basic module packaging.
