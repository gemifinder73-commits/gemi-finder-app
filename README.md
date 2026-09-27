# gemi-finder-app
This POS is free to use
# 📦 Inventory & Receiving Management App

Isang Android/Web application na may direct sync sa **Google Sheets** para sa real-time inventory tracking, receiving item logging, duplicate prevention, at in-app automated updates.

---

## 🚀 Features

- **Item Receiving & Real-Time Sync:**
  - Mabilisang pag-record ng items gamit ang barcode scanning o manual entry.
  - Direktang nag-a-upload sa Google Sheets gamit ang serverless Google Apps Script Web App.
- **Smart Duplicate Prevention:**
  - Bago magdagdag ng bagong row, iche-check ng system ang Barcode sa **Column A**.
  - Kung mayroon na, awtomatikong ia-update ang **Stock (Column E)**, **Price (Column F)**, at **Unit Cost (Column G)** nang walang dobleng record.
- **Header Metadata Support:**
  - Awtomatikong nilalagay ang timestamp sa `F1` (Date Received), at opsyonal na sinusulat ang `B1` (Branch), `B2` (Address), at `F2` (Receipt No.).
- **In-App Auto Update:**
  - May button sa Navigation Drawer Slider: **"Check for App Update"**.
  - Binabasa ang bersyon mula sa Google Sheets (`Update` tab) at awtomatikong dina-download at ini-install ang bagong APK gamit ang Android `DownloadManager` at `FileProvider`.

---

## 📊 Google Sheets Setup

Ang spreadsheet ay dapat may dalawang tabs:

### 1. `Inventory` Tab
Ito ang pangunahing listahan ng mga produkto.

| Column | Header | Description |
| :--- | :--- | :--- |
| **A** | `Barcode` | Unique barcode / SKU ng produkto |
| **B** | `Name` | Pangalan ng item |
| **C** | `Brand` | Brand ng item |
| **D** | `Flavor` | Variant o flavor |
| **E** | `Stock` | Kasalukuyang bilang ng stock |
| **F** | `Price` | Selling Price |
| **G** | `Unit Cost` | Cost Price per unit |

> **Header Details:**
> - `B1`: Branch (Opsyonal)
> - `B2`: Address (Opsyonal)
> - `F1`: Date & Time Received (Awtomatikong nilalagay ng script)
> - `F2`: Receipt No. (Opsyonal)

---

### 2. `Update` Tab
Ginagamit para sa pag-check ng pinakabagong bersyon ng Android APK.

| Cell | Pangalan | Halimbawa |
| :--- | :--- | :--- |
| **B1** | `versionCode` | `2` *(Integer)* |
| **B2** | `versionName` | `v1.0.1` |
| **B3** | `apkUrl` | `https://your-domain.com/releases/app-release.apk` |

---

## ⚙️ Google Apps Script Backend (`Code.gs`)

1. Buksan ang iyong Google Sheet.
2. Pumunta sa **Extensions > Apps Script**.
3. I-paste ang script mula sa [`Code.gs`](./Code.gs).
4. I-click ang **Deploy > Manage deployments > New deployment** (o **Edit > New version**).
5. Siguraduhing naka-set ang:
   - **Execute as:** `Me`
   - **Who has access:** `Anyone`
6. Kopyahin ang nabuong **Web App URL** (`https://script.google.com/macros/s/.../exec`).

---

## 📱 Application Setup & Configuration

### 1. Web App Link Setup
Maaari mong ilagay ang iyong Web App URL sa popup ng **"Add Item Manually"** o i-set ito sa configuration file:

```javascript
const GOOGLE_SCRIPT_URL = "[https://script.google.com/macros/s/.../exec](https://script.google.com/macros/s/.../exec)";
