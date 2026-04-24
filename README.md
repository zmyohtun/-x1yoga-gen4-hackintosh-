# 🍎 Lenovo ThinkPad X1 Yoga Gen 4 — Hackintosh EFI

> **OpenCore bootloader EFI for Lenovo ThinkPad X1 Yoga Gen 4**  
> macOS Ventura / Sonoma compatible

![OpenCore](https://img.shields.io/badge/OpenCore-1.0.x-blue?style=flat-square)
![macOS](https://img.shields.io/badge/macOS-Ventura%20%7C%20Sonoma-brightgreen?style=flat-square)
![Model](https://img.shields.io/badge/Model-X1%20Yoga%20Gen%204-red?style=flat-square)
![Author](https://img.shields.io/badge/author-Dr.%20ZinMyoTun-orange?style=flat-square)

---

## 🇲🇲 မြန်မာဘာသာ ရှင်းလင်းချက်

### Hackintosh ဆိုတာ ဘာလဲ?

**Hackintosh** ဆိုသည်မှာ Apple ကွန်ပျူတာမဟုတ်သော အခြား PC သို့မဟုတ် Laptop တွင် **macOS** တပ်ဆင်၍ အသုံးပြုသောနည်းလမ်းကို ခေါ်သည်။ ဤ repository တွင် **Lenovo ThinkPad X1 Yoga Gen 4** Laptop အတွက် macOS တပ်ဆင်ရာ၌ လိုအပ်သော **EFI partition** ဖိုင်များ ပါဝင်သည်။

### ဤ EFI သည် ဘာအတွက်လဲ?

- **OpenCore** bootloader ဖြင့် macOS ကို boot လုပ်နိုင်ရန် ပြုလုပ်ထားသည်
- Lenovo X1 Yoga Gen 4 ၏ hardware နှင့် macOS ကြား ချိတ်ဆက်ပေးသော kext (driver) များ ပါဝင်သည်
- ACPI patch များ၊ quirks များ မှန်ကန်စွာ သတ်မှတ်ထားသည်

---

### 💻 စက်ပစ္စည်းသတ်မှတ်ချက်

| အစိတ်အပိုင်း | အသေးစိတ် |
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

### ✅ အလုပ်လုပ်သောအရာများ (Working)

- ✅ macOS Ventura / Sonoma boot
- ✅ CPU Power Management (SpeedStep)
- ✅ Intel UHD 620 Graphics (QE/CI)
- ✅ USB ports (USB 3.0 / Type-C)
- ✅ Touchpad & TrackPoint
- ✅ Keyboard (brightness keys, Fn keys)
- ✅ Battery percentage & charging
- ✅ Sleep / Wake
- ✅ Audio (speaker + headphone jack)
- ✅ Webcam
- ✅ Thunderbolt 3
- ✅ HDMI output
- ✅ WiFi (Intel — itlwm)
- ✅ Bluetooth
- ✅ iCloud / App Store / iMessage (SMBIOS ပြင်ဆင်ပြီးနောက်)

---

### ❌ အလုပ်မလုပ်သောအရာများ (Not Working)

- ❌ Fingerprint reader (macOS တွင် TouchID သို့မချိတ်နိုင်)
- ❌ IR Camera (Windows Hello — macOS မထောက်ပံ့)
- ❌ Stylus pen (Wacom — macOS driver မရှိ)

---

### 📁 EFI ဖိုင်တွဲ ဖွဲ့စည်းပုံ

```
EFI/
├── BOOT/
│   └── BOOTx64.efi          # UEFI boot entry
└── OC/
    ├── ACPI/                 # DSDT/SSDT patch ဖိုင်များ
    │   ├── SSDT-PLUG.aml     # CPU power management
    │   ├── SSDT-EC.aml       # Embedded Controller
    │   ├── SSDT-AWAC.aml     # RTC clock fix
    │   └── SSDT-USBX.aml    # USB power
    ├── Drivers/              # OpenCore driver ဖိုင်များ
    │   ├── HfsPlus.efi       # HFS+ filesystem
    │   └── OpenRuntime.efi   # Runtime services
    ├── Kexts/                # macOS kernel extension (driver) များ
    │   ├── Lilu.kext         # Base patcher
    │   ├── WhateverGreen.kext# GPU patch
    │   ├── AppleALC.kext     # Audio
    │   ├── VoodooPS2.kext    # Keyboard/Touchpad
    │   ├── itlwm.kext        # Intel WiFi
    │   └── IntelBTPatcher.kext # Bluetooth
    ├── Resources/            # GUI theme ဖိုင်များ
    ├── Tools/                # OpenCore tools
    └── config.plist          # OpenCore ပင်မ config ဖိုင်
```

---

### 🛠 တပ်ဆင်နည်း (Installation Guide)

#### လိုအပ်သောအရာများ
- USB Drive (16GB နှင့်အထက်)
- [OpenCore](https://github.com/acidanthera/OpenCorePkg) — Bootloader
- macOS installer (App Store သို့မဟုတ် IPSW)
- [ProperTree](https://github.com/corpnewt/ProperTree) — config.plist editor
- [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) — Serial number generator

#### အဆင့်များ

**① BIOS Settings ပြင်ဆင်ပါ**
```
Security → Secure Boot → Disabled
Config → Thunderbolt → Thunderbolt BIOS Assist → Enabled
Config → CPU → Hyperthreading → Enabled
Startup → UEFI/Legacy Boot → UEFI Only
```

**② USB installer ပြုလုပ်ပါ**
```bash
# macOS တွင်
sudo /Applications/Install\ macOS\ Ventura.app/Contents/Resources/createinstallmedia \
  --volume /Volumes/MyUSB
```

**③ EFI partition ထဲသို့ ဤ EFI folder ကူးထည့်ပါ**
```bash
# USB ၏ EFI partition mount လုပ်ပါ
sudo diskutil mount EFI
# ဤ repo မှ EFI folder ကူးထည့်ပါ
cp -r EFI/ /Volumes/EFI/
```

**④ SMBIOS သတ်မှတ်ပါ** *(iCloud / iMessage အသုံးပြုလိုပါက)*
```
GenSMBIOS ဖြင့် MacBookPro15,2 SMBIOS generate လုပ်ပြီး
config.plist → PlatformInfo → Generic တွင် ထည့်သွင်းပါ
```

**⑤ Boot လုပ်ပါ**
- USB မှ boot လုပ်၍ macOS Installer ကို ရွေးပါ
- Disk Utility → APFS format → Install macOS

---

### ⚙️ OpenCore Config အကြောင်း

`config.plist` သည် OpenCore ၏ အဓိက ပြင်ဆင်မှုဖိုင်ဖြစ်သည်။ ပြင်ဆင်ရာတွင် —

- **ProperTree** သုံး၍ ပြင်ပါ (Text editor ဖြင့် မပြင်ပါနှင့်)
- `PlatformInfo` section တွင် သင်၏ SMBIOS data ထည့်ရမည်
- Debug log လိုပါက `Misc → Debug → AppleDebug = true` သတ်မှတ်ပါ

---

### 🔄 Update လုပ်နည်း

OpenCore version အသစ်ထွက်တိုင်း —
1. [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg/releases) မှ latest release ဒေါင်းလုပ်ပါ
2. Kext များကို [Lilu-and-Friends](https://github.com/corpnewt/Lilu-and-Friends) ဖြင့် update လုပ်ပါ
3. config.plist ကို [OCConfigCompare](https://github.com/corpnewt/OCConfigCompare) ဖြင့် စစ်ဆေးပါ

---

### ❓ အကူအညီ

ပြဿနာရှိပါက —
- [Dortania Guide](https://dortania.github.io/OpenCore-Install-Guide/) — အသေးစိတ် တပ်ဆင်လမ်းညွှန်
- [r/hackintosh](https://reddit.com/r/hackintosh) — Community forum
- GitHub Issues တွင် report တင်ပါ

---

## ⚠️ သတိပေးချက်

> ဤ EFI သည် **Lenovo ThinkPad X1 Yoga Gen 4** အတွက်သာ ဖြစ်သည်။  
> အခြား model များတွင် တိုက်ရိုက် အသုံးပြုခြင်း **မပြုပါနှင့်**။  
> Config ကို ကိုယ်တိုင် verify မလုပ်မီ Serial Number **မပြောင်းပါနှင့်**။

---

## 👨‍💻 ရေးသားသူ

**Dr. ZinMyoTun**  
GitHub: [@zmyohtun](https://github.com/zmyohtun)

---

## 📄 License

For educational purposes only. macOS is property of Apple Inc.
