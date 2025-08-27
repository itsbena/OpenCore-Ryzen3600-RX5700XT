# OpenCore EFI for MSI B450 Gaming Plus Max, Ryzen 5 3600 and RX 5700 XT

This repository contains my personal **OpenCore EFI** configuration for the following hardware:

- **CPU:** AMD Ryzen 5 3600  
- **GPU:** Radeon RX 5700 XT 8GB  
- **RAM:** 4 × 8GB DDR4 3200MHz CL16  
- **Motherboard:** MSI B450 Gaming Plus Max  

---

## ✅ Tested macOS versions
- Ventura  
- Sonoma  
- Sequoia  

Based on **OpenCore 1.0.5**.

---

## ⚠️ Disclaimer
- This EFI is designed **only for this hardware**.  
- Having the same hardware does **not guarantee** that this EFI will work for you.  
- I do **not provide support**.  

If you run into issues, please check the official OpenCore Troubleshooting Guide:  
👉 [OpenCore Troubleshooting](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/troubleshooting.html#table-of-contents)

---

## 🔧 Installation Guide

Follow the official OpenCore USB installer creation guide:  
👉 [Creating the USB Installer](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)

When you reach the step to add the EFI folder, use the one from this repository and **modify your `config.plist`** as follows:

### Generate SMBIOS (iMacPro1,1)
Use [GenSMBIOS](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html#platforminfo) to generate a new SMBIOS.  
Update your `config.plist` with these values:

- `Generic -> SystemProductName` → **Type**  
- `Generic -> SystemSerialNumber` → **Serial**  
- `Generic -> MLB` → **Board Serial**  
- `Generic -> SystemUUID` → **SmUUID**  
- `Generic -> ROM` → Your network card’s **MAC address** (without dots, spaces, or hyphens)

---

### USB Mapping
Before installation, you **must** map your USB ports using:  
👉 [USBToolBox](https://github.com/USBToolBox/tool)  

- Place the generated kext inside the `Kexts` folder.  
- Add it to your `config.plist` using **OC Snapshot** in [ProperTree](https://github.com/corpnewt/ProperTree) or manually.  

---

### BIOS Settings
Update your BIOS to the latest version and configure it as follows:

- Disable **CSM**  
- Disable **Secure Boot**  
- Disable **Serial Port**  
- Disable **Parallel Port**  
- Set **SATA Mode** → AHCI  
- Enable **XHCI Hand-off**  
- Enable **SVM**  

---

### Installation Process
Follow the official OpenCore installation guide:  
👉 [macOS Installation](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html)

After installation:  
1. Use [EFI Mounter](https://www.dualbootpc.com/software/utility/efi-mounter-v3/) to mount the EFI partition of your drive.  
2. Copy the EFI folder from the USB installer to the disk’s EFI partition.  
3. Edit your `config.plist` and set:  
   - `Misc -> Security -> SecureBootModel` → **Default**

---

## 🖥️ Post-Install
- **Dual boot configuration:** [Guide](https://dortania.github.io/OpenCore-Post-Install/multiboot/bootstrap.html)  
- **Fix iServices (iCloud, iMessage, etc.):** [Guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html)  

---

## 🐞 Debugging
To enable debugging, modify your `config.plist` as follows:

- `Misc -> Debug`  
  - `AppleDebug` → **True**  
  - `ApplePanic` → **True**  
  - `Target` → **67**  

- `NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 -> boot-args`  
  Add: `-v keepsyms=1 debug=0x100`
