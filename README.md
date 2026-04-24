# 🍎 Lenovo ThinkPad X1 Yoga Gen 4 — Hackintosh EFI

> **OpenCore bootloader EFI for Lenovo ThinkPad X1 Yoga Gen 4**  
> macOS Ventura / Sonoma compatible

![OpenCore](https://img.shields.io/badge/OpenCore-1.0.x-blue?style=flat-square)
![macOS](https://img.shields.io/badge/macOS-Ventura%20%7C%20Sonoma-brightgreen?style=flat-square)
![Model](https://img.shields.io/badge/Model-X1%20Yoga%20Gen%204-red?style=flat-square)
![Author](https://img.shields.io/badge/author-Dr.%20ZinMyoTun-orange?style=flat-square)

---

## 🇲🇲 မြန်မာဘာသာ | 🌐 English

---

### Hackintosh ဆိုတာ ဘာလဲ? / What is Hackintosh?

🇲🇲 **Hackintosh** ဆိုသည်မှာ Apple ကွန်ပျူတာမဟုတ်သော အခြား PC သို့မဟုတ် Laptop တွင် **macOS** တပ်ဆင်၍ အသုံးပြုသောနည်းလမ်းကို ခေါ်သည်။ ဤ repository တွင် **Lenovo ThinkPad X1 Yoga Gen 4** Laptop အတွက် macOS တပ်ဆင်ရာ၌ လိုအပ်သော **EFI partition** ဖိုင်များ ပါဝင်သည်။

🌐 **Hackintosh** refers to installing **macOS** on non-Apple hardware — a regular PC or laptop. This repository contains the **EFI partition files** needed to boot macOS on a **Lenovo ThinkPad X1 Yoga Gen 4** using the OpenCore bootloader.

---

### ဤ EFI သည် ဘာအတွက်လဲ? / What does this EFI do?

🇲🇲
- **OpenCore** bootloader ဖြင့် macOS ကို boot လုပ်နိုင်ရန် ပြုလုပ်ထားသည်
- Lenovo X1 Yoga Gen 4 ၏ hardware နှင့် macOS ကြား ချိတ်ဆက်ပေးသော kext (driver) များ ပါဝင်သည်
- ACPI patch များ၊ quirks များ မှန်ကန်စွာ သတ်မှတ်ထားသည်

🌐
- Enables macOS to **boot via OpenCore** bootloader
- Includes **kexts (drivers)** that bridge the gap between X1 Yoga Gen 4 hardware and macOS
- Contains correctly configured **ACPI patches** and OpenCore quirks

---

### 💻 စက်ပစ္စည်းသတ်မှတ်ချက် / Hardware Specifications

| အစိတ်အပိုင်း / Component | အသေးစိတ် / Details |
|---|---|
| **Model** | Lenovo ThinkPad X1 Yoga Gen 4 (2019) |
| **CPU** | Intel Core i5/i7 8th Gen (Whiskey Lake) |
| **GPU** | Intel UHD Graphics 620 |
| **RAM** | 8GB / 16GB LPDDR3 |
| **Storage** | NVMe SSD |
| **Display** | 14" FHD / WQHD IPS Touch |
| **WiFi** | Intel Wireless-AC 9560 |
| **Bluetooth** | Intel Bluetooth 5.0 |
| **Audio** | Realtek ALC285 |
| **Touchpad** | Synaptics TrackPoint + Touchpad |

---

### ✅ အလုပ်လုပ်သောအရာများ / What Works

🇲🇲 အောက်ပါ hardware/feature များ macOS တွင် အပြည့်အဝ အလုပ်လုပ်သည် —

🌐 The following hardware and features work fully under macOS —

- ✅ macOS Ventura / Sonoma boot
- ✅ CPU Power Management — SpeedStep (အမြန်နှုန်းညှိခြင်း / frequency scaling)
- ✅ Intel UHD 620 Graphics — QE/CI acceleration (ဂရပ်ဖစ် အပြည့်ထောက်ပံ့မှု / full GPU acceleration)
- ✅ USB ports — USB 3.0 / Type-C
- ✅ Touchpad & TrackPoint
- ✅ Keyboard — brightness keys, Fn keys
- ✅ Battery percentage & charging (ဘက်ထရီ ရာနှုန်း / battery status)
- ✅ Sleep / Wake (အိပ်ပျော်ခြင်း-နိုးထခြင်း / sleep-wake cycle)
- ✅ Audio — speaker + headphone jack (ဒေါင်းစပီကာ + နားကြပ်ပေါက် / built-in audio)
- ✅ Webcam
- ✅ Thunderbolt 3
- ✅ HDMI output (ပြင်ပမော်နီတာ / external display)
- ✅ WiFi — Intel via `itlwm.kext`
- ✅ Bluetooth
- ✅ iCloud / App Store / iMessage *(SMBIOS ပြင်ဆင်ပြီးနောက် / after SMBIOS setup)*

---

### ❌ အလုပ်မလုပ်သောအရာများ / What Does Not Work

🇲🇲 အောက်ပါ feature များ macOS တွင် ထောက်ပံ့မှုမရှိ —

🌐 The following features are not supported under macOS —

| Feature | မြန်မာ ရှင်းလင်းချက် | English Reason |
|---|---|---|
| Fingerprint reader | macOS တွင် TouchID သို့ မချိတ်နိုင် | Cannot link to macOS TouchID |
| IR Camera | Windows Hello — macOS မထောက်ပံ့ | Windows Hello only, no macOS driver |
| Stylus pen (Wacom) | macOS Wacom driver မရှိ | No macOS driver available |

---

### 📁 EFI ဖိုင်တွဲ ဖွဲ့စည်းပုံ / EFI Folder Structure

🇲🇲 ဤ EFI folder ၏ ဖွဲ့စည်းပုံ —  
🌐 Layout of this EFI folder —

```
EFI/
├── BOOT/
│   └── BOOTx64.efi              # UEFI boot entry point
└── OC/
    ├── ACPI/                    # DSDT/SSDT patches
    │   ├── SSDT-PLUG.aml        # CPU power management (CPU အမြန်နှုန်းစီမံ)
    │   ├── SSDT-EC.aml          # Embedded Controller fix
    │   ├── SSDT-AWAC.aml        # RTC clock fix
    │   └── SSDT-USBX.aml        # USB power management
    ├── Drivers/                 # OpenCore EFI drivers
    │   ├── HfsPlus.efi          # HFS+ filesystem support
    │   └── OpenRuntime.efi      # Runtime services
    ├── Kexts/                   # macOS kernel extensions (drivers)
    │   ├── Lilu.kext            # Core patcher — all kexts depend on this
    │   ├── WhateverGreen.kext   # GPU / display patch (ဂရပ်ဖစ်ပြင်ဆင်မှု)
    │   ├── AppleALC.kext        # Audio codec (အသံကတ် driver)
    │   ├── VoodooPS2.kext       # Keyboard & Touchpad (ကီးဘုတ် + ထိတွေ့ပြားl)
    │   ├── itlwm.kext           # Intel WiFi driver
    │   └── IntelBTPatcher.kext  # Intel Bluetooth fix
    ├── Resources/               # OpenCore GUI theme files
    ├── Tools/                   # OpenCore utility tools
    └── config.plist             # Main OpenCore configuration file (ပင်မ config ဖိုင်)
```

---

### 🛠 တပ်ဆင်နည်း / Installation Guide

#### လိုအပ်သောအရာများ / Prerequisites

🇲🇲 တပ်ဆင်မည့်မတိုင်မီ အောက်ပါ tool များ လိုအပ်သည် —  
🌐 You will need the following tools before starting —

- **USB Drive** — 16GB နှင့်အထက် / 16GB or larger
- **[OpenCore](https://github.com/acidanthera/OpenCorePkg)** — Bootloader
- **macOS Installer** — App Store or IPSW
- **[ProperTree](https://github.com/corpnewt/ProperTree)** — config.plist ပြင်ရန် / config editor
- **[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)** — Serial number ဆောက်ရန် / SMBIOS generator

---

#### အဆင့်များ / Steps

**① BIOS Settings ပြင်ဆင်ပါ / Configure BIOS**

🇲🇲 Laptop ဖွင့်ပြီး `F1` နှိပ်၍ BIOS ဝင်ပါ၊ အောက်ပါ option များ ပြောင်းပါ —  
🌐 Boot into BIOS by pressing `F1` at startup and set the following —

```
Security  → Secure Boot            → Disabled
Config    → Thunderbolt BIOS Assist → Enabled
Config    → CPU → Hyperthreading   → Enabled
Startup   → UEFI/Legacy Boot       → UEFI Only
```

---

**② USB installer ပြုလုပ်ပါ / Create macOS USB Installer**

🇲🇲 macOS တွင် Terminal ဖွင့်၍ —  
🌐 Open Terminal on macOS and run —

```bash
sudo /Applications/Install\ macOS\ Ventura.app/Contents/Resources/createinstallmedia \
  --volume /Volumes/MyUSB
```

---

**③ EFI ဖိုင် ကူးထည့်ပါ / Copy EFI to USB**

🇲🇲 USB ၏ EFI partition ထဲသို့ ဤ repo ၏ EFI folder ကူးထည့်ပါ —  
🌐 Mount the USB EFI partition and copy this repo's EFI folder into it —

```bash
sudo diskutil mount EFI
cp -r EFI/ /Volumes/EFI/
```

---

**④ SMBIOS သတ်မှတ်ပါ / Set Up SMBIOS** *(iCloud / iMessage / FaceTime အတွက် / required for Apple services)*

🇲🇲 GenSMBIOS ဖြင့် `MacBookPro15,2` SMBIOS generate လုပ်ပြီး `config.plist → PlatformInfo → Generic` တွင် ထည့်ပါ —  
🌐 Use GenSMBIOS to generate a `MacBookPro15,2` SMBIOS and paste it into `config.plist → PlatformInfo → Generic` —

> ⚠️ **မြန်မာ:** ရရှိသော Serial Number ကို online စစ်ဆေးပြီး "Purchase Date not Validated" ပြမှသာ သုံးပါ။  
> ⚠️ **English:** Always verify your generated serial on [Apple's Check Coverage](https://checkcoverage.apple.com) page — use it only if it shows "Purchase Date not Validated."

---

**⑤ Boot လုပ်ပါ / Boot macOS**

🇲🇲 USB မှ boot လုပ်၍ OpenCore picker တွင် macOS Installer ကို ရွေးပါ → Disk Utility → APFS format → Install macOS  
🌐 Boot from USB → select macOS Installer in OpenCore picker → Disk Utility → format as APFS → Install macOS

---

### ⚙️ OpenCore Config အကြောင်း / About config.plist

🇲🇲 `config.plist` သည် OpenCore ၏ အဓိက ပြင်ဆင်မှုဖိုင်ဖြစ်သည်။ ပြင်ဆင်ရာတွင် —  
🌐 `config.plist` is the main OpenCore configuration file. When editing —

- 🇲🇲 **ProperTree** သာ သုံးပါ — plain text editor ဖြင့် ပြင်ပါက format ပျက်နိုင်သည်  
  🌐 Use **ProperTree** only — editing with a plain text editor risks breaking the XML structure
- 🇲🇲 `PlatformInfo` section တွင် သင်၏ SMBIOS data ထည့်ရမည်  
  🌐 Insert your SMBIOS data in the `PlatformInfo` section
- 🇲🇲 Debug log ကြည့်လိုပါက `Misc → Debug → AppleDebug = true` သတ်မှတ်ပါ  
  🌐 Enable `Misc → Debug → AppleDebug = true` to capture verbose boot logs for troubleshooting

---

### 🔄 Update လုပ်နည်း / How to Update

🇲🇲 OpenCore version အသစ်ထွက်တိုင်း အောက်ပါ အဆင့်များ လိုက်နာပါ —  
🌐 Follow these steps each time a new OpenCore version is released —

1. 🇲🇲 [OpenCorePkg Releases](https://github.com/acidanthera/OpenCorePkg/releases) မှ latest ဒေါင်းလုပ်ပါ  
   🌐 Download the latest release from [OpenCorePkg Releases](https://github.com/acidanthera/OpenCorePkg/releases)

2. 🇲🇲 Kext များကို [Lilu-and-Friends](https://github.com/corpnewt/Lilu-and-Friends) ဖြင့် update လုပ်ပါ  
   🌐 Update all kexts using [Lilu-and-Friends](https://github.com/corpnewt/Lilu-and-Friends)

3. 🇲🇲 config.plist ကို [OCConfigCompare](https://github.com/corpnewt/OCConfigCompare) ဖြင့် စစ်ဆေးပါ  
   🌐 Compare your config.plist against the new sample using [OCConfigCompare](https://github.com/corpnewt/OCConfigCompare)

---

### ❓ အကူအညီ / Getting Help

🇲🇲 ပြဿနာရှိပါက အောက်ပါ နေရာများတွင် ရှာဖွေနိုင်သည် —  
🌐 If you encounter issues, refer to —

- 📖 [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) — အသေးစိတ် တပ်ဆင်လမ်းညွှန် / comprehensive installation guide
- 💬 [r/hackintosh](https://reddit.com/r/hackintosh) — Community forum
- 🐛 GitHub Issues — ဤ repo တွင် report တင်ပါ / file a bug report in this repo

---

## ⚠️ သတိပေးချက် / Disclaimer

🇲🇲
> ဤ EFI သည် **Lenovo ThinkPad X1 Yoga Gen 4** အတွက်သာ ဖြစ်သည်။ အခြား model များတွင် တိုက်ရိုက် အသုံးပြုခြင်း **မပြုပါနှင့်**။ Config ကို ကိုယ်တိုင် verify မလုပ်မီ Serial Number **မပြောင်းပါနှင့်**။

🌐
> This EFI is built specifically for the **Lenovo ThinkPad X1 Yoga Gen 4**. Do **not** use it directly on other models without proper verification. Do **not** share or reuse serial numbers — always generate your own unique SMBIOS.

---

## 👨‍💻 ရေးသားသူ / Author

**Dr. ZinMyoTun**  
GitHub: [@zmyohtun](https://github.com/zmyohtun)

---

## 📄 License

For educational purposes only. macOS is the property of Apple Inc.  
*(ပညာရေးရည်ရွယ်ချက်ဖြင့်သာ — macOS သည် Apple Inc. ပိုင်ဆိုင်သည်)*
