# Kali NetHunter Kernel for Miatoll (Snapdragon 720G)

> **Kali NetHunter kernel for Xiaomi Miatoll devices with WiFi injection, USB adapter support, and penetration testing capabilities.**

Custom **Kali NetHunter Kernel** built on the **OpenELA / Stormbreaker** Linux 4.14 (`4.14.357`) source tree, specifically tailored for the **Xiaomi Miatoll** device family. This kernel includes full wireless penetration testing capabilities, including **WiFi packet injection**, USB WiFi adapter support, and stability fixes.

---

## 📱 Supported Devices (`miatoll`)

This kernel uses a universal installer supporting the following devices powered by the **Qualcomm Snapdragon 720G (SM6250)** platform:

| Device Codename | Commercial Name |
| --------------- | --------------- |
| `curtana`       | Redmi Note 9S / Redmi Note 9 Pro (India) |
| `joyeuse`       | Redmi Note 9 Pro (Global) |
| `excalibur`     | Redmi Note 9 Pro Max |
| `gram`          | POCO M2 Pro |

---

## ⚡ Key Features & Highlights

- **Kernel Version:** Linux `4.14.357-openela-Stormbreaker-NetHunter-miatoll`
- **Kali NetHunter Ready:** Full native support for `/lib/modules` (non-systemless installation for reliable NetHunter app integration).
- **Wireless Penetration Testing:**
  - **WiFi Packet Injection** patches applied.
  - **rtw88** driver support.
- **Stability & Fixes:**
  - Includes netdev notifier crash fixes on USB WiFi disconnect (`prima-fix-netdev-crash`).
- **Flasher:** Packaged with **AnyKernel3** by `osm0sis` for safe and seamless flashing across different ROMs (MIUI / AOSP / Custom ROMs).

---

## 📦 What's Included in the Release Zip

The AnyKernel3 zip package (`anykernel-nethunter-miatoll-<date>.zip`) contains:
- `Image.gz-dtb` — Compiled kernel image bundled with Device Tree Blob.
- `anykernel.sh` — Automated installation script that backs up your current boot image and patches ramdisk properties.
- `modules/` — Kernel modules (`.ko`) installed directly to `/lib/modules/`, including:
  - `rmnet_shs.ko` & `rmnet_perf.ko` (Qualcomm data drivers)
  - `gspca_main.ko` (USB camera/webcam support)
- `Changelog.txt` — Detailed commit history and daily updates.

---

## 📋 Prerequisites

Before flashing this kernel, ensure your device meets the following requirements:

1. **Unlocked Bootloader**
2. **Custom Recovery Installed:** TWRP, OrangeFox, or PitchBlack Recovery.
3. **Backup:** Always take a full Nandroid backup (Boot, DTBO, and Vendor/System) in recovery before flashing custom kernels.
4. **Magisk:** Recommended to manage root permissions and run Kali NetHunter app features correctly.

---

## 📥 Installation Instructions

1. **Download** the latest `anykernel-nethunter-miatoll-*.zip` from the [Releases](../../releases) page.
2. **Transfer** the zip file to your phone's internal storage or SD card.
3. **Reboot to Recovery** (Power Off -> Volume Up + Power Button).
4. **Flash the Zip:**
   - Tap on **Install** / **Select Zip**.
   - Navigate to `anykernel-nethunter-miatoll-*.zip`.
   - Swipe to confirm flash.
5. **Wipe Cache/Dalvik** (Optional, but recommended after kernel changes).
6. **Reboot System**.

---

## 🛠️ Building from Source / Contributing

If you wish to compile or modify this kernel:
- **Base Source:** OpenELA / Stormbreaker Linux 4.14 tree.
- **Toolchain:** Clang / GCC compatible with Snapdragon 720G architecture.
- Feel free to open issues or submit pull requests for bug fixes or optimizations!

---

## 🤝 Credits & Acknowledgements

- **Kali NetHunter Team** for the NetHunter project & Re4son for installation scripts.
- **osm0sis** for **AnyKernel3**.
- **OpenELA & Stormbreaker Developers** for the robust 4.14 kernel source and device trees.
- Xiaomi / Miatoll kernel contributors and community testers.
