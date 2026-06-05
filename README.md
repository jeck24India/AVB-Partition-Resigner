# ⚡ High-Speed AVB Partition Resigner

A standalone, portable high-performance Windows utility (`.exe`) designed to patch, re-sign, and synchronize Android image files utilizing Google's Android Verified Boot (AVB) structure. 

---

## 🚀 Intelligent Device Matrix

* **📟 Universal Signing (All Devices):** Fully compatible across **all Android devices** for raw partitions (like `boot.img`). As long as you provide a valid private key, the tool instantly strips the old footer and re-signs the target file without structural changes.
* **🐉 Lenovo Global Converter:** Automatically triggered when processing a `vendor_boot` partition. It hot-swaps internal region headers (`IROW` to `IPRC`) to seamlessly adapt Lenovo images to Global configurations before applying the cryptographic signature.

---

## 🛠️ Requirements & Workspace Setup

To run the tool, simply place these two companion files in the **exact same folder**:

1. **`sign_tool.exe`** — The main compiled executable utility.
2. **`avbtool.py`** — Google's structural script dependency (must sit right next to the EXE).

*Note: Your users do **not** need to install Python to use this executable wrapper.*

---

## 🚦 Execution Examples (Command Prompt / Powershell)

Open your terminal inside your working tool directory and run the commands using this syntax:
```cmd
sign_tool.exe <PATH_TO_TARGET_IMAGE> <PATH_TO_PRIVATE_KEY> [PATH_TO_VBMETA_IMAGE]
```

### 🔹 Example 1: Universal Sign Only (Any Device / Any Partition)
Skips binary patching and applies a clean cryptographic signature:
```cmd
sign_tool.exe boot.img custom_private_key.pem
```

### 🔹 Example 2: Lenovo Global Conversion + Sign
Automatically detects `vendor_boot`, executes the hex-swap layout conversion patch, and signs:
```cmd
sign_tool.exe vendor_boot.img custom_private_key.pem
```

### 🔹 Example 3: Full Chain Re-sign & VBMeta Integration
Appends descriptors and chains your signatures directly back to a root verification file:
```cmd
sign_tool.exe boot.img custom_private_key.pem vbmeta.img
```
*Outputs a fully compiled and chained verification block saved as `vbmeta_final.img`.*

---

## 🤝 Support Details

If you encounter breaking structural image updates or need deployment troubleshooting:

* **Official Channel:** [Telegram Chat Link](https://t.me/rom2box_updates) 

---

## ⚠️ Disclaimer
Tampering with Android Verified Boot parameters requires unlocked system bootloaders. Creating improper descriptors or key chain mismatches will drop the hardware directly into a secure boot loop interface. Ensure you maintain full baseline physical ROM backups before testing.
