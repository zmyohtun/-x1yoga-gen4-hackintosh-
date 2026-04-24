# Lenovo ThinkPad X1 Yoga Gen 4 — Hackintosh EFI (OpenCore)

[![macOS](https://img.shields.io/badge/macOS-Sequoia%2015.7.5-brightgreen)](https://www.apple.com/macos/sequoia/)
[![OpenCore](https://img.shields.io/badge/OpenCore-Latest-blue)](https://github.com/acidanthera/OpenCorePkg)
[![SMBIOS](https://img.shields.io/badge/SMBIOS-MacBookPro15%2C2-orange)](https://support.apple.com/en-us/111893)
[![Status](https://img.shields.io/badge/Status-Working-success)](#)

> OpenCore EFI for Lenovo ThinkPad X1 Yoga 4th Generation running macOS Sequoia 15.7.5

---

## 💻 Hardware Specifications

| Component | Details |
|-----------|---------|
| **Model** | Lenovo ThinkPad X1 Yoga Gen 4 |
| **CPU** | Intel Core i7-8565U (Whiskey Lake, 4C/8T) |
| **iGPU** | Intel UHD Graphics 620 |
| **RAM** | 16 GB LPDDR3 |
| **Storage** | KINGBANK NVMe SSD |
| **Display** | 14" FHD IPS Touchscreen (1920×1080) |
| **WiFi / BT** | Intel Wireless-AC 9560 (WiFi + Bluetooth) |
| **Audio** | Realtek ALC285 |
| **Ethernet** | Intel I219-V |
| **Trackpad** | I2C (VoodooI2C) |
| **Touchscreen** | I2C HID (VoodooI2CHID) |

---

## ✅ What Works

| Feature | Status | Notes |
|---------|--------|-------|
| macOS Sequoia 15.7.5 | ✅ Working | Stable boot |
| Intel UHD 620 iGPU | ✅ Working | Full acceleration |
| Audio (Speakers) | ✅ Working | ALC285, layout-id 71 |
| WiFi | ✅ Working | itlwm + HeliPort |
| Ethernet | ✅ Working | Intel I219-V |
| Trackpad | ✅ Working | I2C, multi-gesture |
| Touchscreen | ✅ Working | Full touch + stylus |
| Battery | ✅ Working | % indicator + status |
| Brightness Keys | ✅ Working | Fn+F5/F6 |
| Sleep / Wake | ✅ Working | SSDT-GPRW fix |
| USB Ports | ✅ Working | Custom USB map |
| Thunderbolt (USB-C) | ✅ Working | USB mode |
| NVMe SSD | ✅ Working | With ASPM fix |
| CPU Power Management | ✅ Working | CPUFriend tuned |
| Fan Control | ✅ Working | YogaSMC |
| Backlight Control | ✅ Working | SSDT-PNLF |

---

## ❌ What Doesn't Work

| Feature | Status | Notes |
|---------|--------|-------|
| Bluetooth | ⚠️ Partial | Intel 9560 BT — varies by macOS version |
| Internal Microphone | ❌ Not Working | Intel SST DSP — no macOS driver exists |
| FaceTime Camera | ⚠️ Check permissions | USB detected; enable in Privacy & Security |
| Fingerprint Reader | ❌ Not Working | No macOS driver |
| Thunderbolt 3 (full) | ❌ Not Working | TB3 hotplug not supported |
| HDMI Audio | ❌ Not tested | |

---

## 🧩 Kexts Used

| Kext | Version | Purpose |
|------|---------|---------|
| Lilu | 1.7.2 | Patch engine (required) |
| VirtualSMC | 1.3.7 | SMC emulator |
| WhateverGreen | 1.7.0 | iGPU patches |
| AppleALC | 1.9.7 | Audio (ALC285, layout 71) |
| IntelMausi | 1.0.8 | Ethernet |
| NVMeFix | 1.1.3 | NVMe power management |
| CPUFriend | 1.3.0 | CPU power management |
| CPUFriendDataProvider | Custom | Balance Power profile |
| ECEnabler | 1.0.6 | Battery EC registers |
| USBMap | Custom | 12-port USB map |
| VoodooI2C | 2.9.1 | I2C trackpad + touchscreen |
| VoodooI2CHID | 1.0 | HID touchscreen |
| VoodooPS2Controller | 2.3.7 | Keyboard |
| itlwm | 2.3.0 | Intel WiFi (use with HeliPort) |
| IntelBluetoothFirmware | 2.4.0 | Intel BT firmware |
| IntelBTPatcher | 2.4.0 | BT stack patch (Sequoia) |
| BlueToolFixup | 2.7.2 | BT fix (Monterey+) |
| BrightnessKeys | Latest | Fn brightness keys |
| YogaSMC | 1.5.3 | ThinkPad fan + power |
| SMCBatteryManager | 1.3.7 | Battery status |
| SMCProcessor | 1.3.7 | CPU temp sensor |
| SMCLightSensor | 1.3.7 | Ambient light |

---

## 📂 ACPI SSDTs

| File | Purpose |
|------|---------|
| SSDT-PLUG | CPU power management (XCPM) |
| SSDT-EC-USBX | Embedded controller + USB power |
| SSDT-AWAC | System clock fix |
| SSDT-PMC | NVRAM fix |
| SSDT-PNLF | Backlight control |
| SSDT-GPIO | VoodooI2C GPIO interrupt mode |
| SSDT-XOSI | Windows compatibility (I2C) |
| SSDT-HPET | IRQ conflict fix |
| SSDT-GPRW | Sleep instant-wake fix |
| SSDT-DMIC | Digital mic enable |

---

## ⚙️ BIOS Settings

Before installing, configure BIOS (press F1 at startup):

**Disable:**
- Secure Boot
- Fast Boot
- CSM / Legacy Boot
- Intel SGX

**Enable:**
- UEFI Boot
- VT-x (Virtualization)
- UEFI Network Stack (optional)

---

## 🚀 Installation

### 1. Generate your own SMBIOS
This EFI ships with **placeholder serial numbers**. You **must** generate unique values before use.

Using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS):
```
SMBIOS type: MacBookPro15,2
```

Fill these fields in `config.plist` → `PlatformInfo → Generic`:
- `SystemSerialNumber`
- `MLB`
- `SystemUUID`
- `ROM` (your ethernet MAC address, no colons)

### 2. Set up WiFi
This EFI uses **itlwm + HeliPort** for WiFi:
1. Download [HeliPort](https://github.com/OpenIntelWireless/HeliPort/releases)
2. Add to Login Items for auto-connect on boot
3. Connect to your network via the HeliPort menu bar icon

### 3. After First Boot
Run these in Terminal for better battery life:
```bash
sudo pmset -a proximitywake 0
sudo pmset -a tcpkeepalive 0
sudo pmset -a powernap 0
```

Enable camera in **System Settings → Privacy & Security → Camera → FaceTime**.

---

## 🔧 Key Config Notes

| Setting | Value | Reason |
|---------|-------|--------|
| SMBIOS | MacBookPro15,2 | Best match for Whiskey Lake |
| `alcid` | 71 | ALC285 speaker output |
| `darkwake` | 0 | Prevent sleep battery drain |
| `proximitywake` | 0 | Prevent Handoff wake events |
| `hibernatemode` | 0 | Disable hibernation |
| `-nvmefaspm` | on | Fix NVMe ASPM on Hackintosh |
| Booter | EnableWriteUnprotector=True | Required for Lenovo firmware |

---

## 📋 Broadcom Bluetooth Dongle (Optional)

For reliable Bluetooth on Sequoia, an **ASUS USB-BT500** or **ASUS USB-BT400** (BCM20702A0 chip) is recommended.

When dongle arrives:
1. Enable `BrcmPatchRAM3.kext` and `BrcmFirmwareData.kext` in config.plist
2. Disable `IntelBluetoothFirmware.kext` and `IntelBTPatcher.kext`
3. Reboot

---

## 🙏 Credits

- [Acidanthera](https://github.com/acidanthera) — OpenCore, Lilu, WhateverGreen, AppleALC, VirtualSMC, CPUFriend
- [OpenIntelWireless](https://github.com/OpenIntelWireless) — itlwm, IntelBluetoothFirmware
- [VoodooI2C](https://github.com/VoodooI2C) — Touchscreen & Trackpad
- [Dortania](https://dortania.github.io/OpenCore-Install-Guide/) — OpenCore Install Guide
- [YogaSMC](https://github.com/zhen-zen/YogaSMC) — ThinkPad power management
- [CorpNewt](https://github.com/corpnewt) — GenSMBIOS, ProperTree tools

---

## ⚠️ Disclaimer

This EFI is for **educational and personal use only**. macOS is proprietary software by Apple Inc. Use on non-Apple hardware may violate Apple's EULA. The author is not responsible for any damage to your device.

---

*Tested on: Lenovo ThinkPad X1 Yoga Gen 4 | macOS Sequoia 15.7.5 | OpenCore*
