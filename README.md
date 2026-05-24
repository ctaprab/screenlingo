# 🎮 ScreenLingo

**ScreenLingo** is a browser-based live OCR overlay tool for gamers. It captures your game window, reads on-screen text using OCR, and displays it in a clean draggable panel — so you can read game dialog in any language without leaving the game.

---

## ✨ Features

- 📺 **Screen capture** — capture any game window directly in the browser
- ✏️ **Region selection** — draw a box over the dialog area for precise OCR
- 🔍 **Auto scan loop** — scans every N seconds, only updates when text changes
- 🧹 **Smart noise filtering** — removes UI chrome, symbols, and short noise tokens
- ⬜ **White text mode** — preprocesses image for white-on-dark text (inverts + thresholds)
- 📖 **Draggable text panel** — floats over the preview, resizable, adjustable font size
- 🇹🇭🇬🇧🇯🇵 **Multi-language OCR** — supports English, Thai, and Japanese
- 🚫 **Duplicate skip** — fingerprints Thai/English/Japanese content to skip repeat scans
- 🌐 **Thai UI** — all buttons and instructions in Thai

---

## 🚀 How to Use

### 1. Open with Chrome (CORS bypass required)

```cmd
"C:\Program Files\Google\Chrome\Application\chrome.exe" --disable-web-security --user-data-dir="C:\ChromeDev" --allow-file-access-from-files "C:\PATH\TO\screenlingo-simple.html"
```

### 2. Steps inside the app

1. คลิก **📺 จับภาพหน้าจอ** → เลือกหน้าต่างเกม
2. คลิก **✏️ กำหนดพื้นที่** → ลากครอบกล่องบทสนทนา
3. คลิก **▶ เริ่มสแกน** → OCR จะอ่านข้อความอัตโนมัติ
4. ข้อความจะแสดงในกล่องลาก-วางได้ด้านล่าง
5. คลิกขวาที่กล่องข้อความ → **แปลภาษา** ใน Chrome เพื่อแปลเป็นภาษาไทย

---

## 📋 Requirements

- **Google Chrome** (any modern version)
- No installation, no server, no API key needed
- Internet connection (for OCR language pack download on first use)

---

## 📁 Files

| File | Description |
|------|-------------|
| `screenlingo-simple.html` | Main app — single file, open directly in Chrome |
| `README.md` | This file |

---

## ⚙️ Settings

| Setting | Description |
|---------|-------------|
| ทุก N วินาที | Scan interval (2–15 seconds) |
| ⬜ ข้อความสีขาว | White text mode — best for light text on dark backgrounds |
| 📖 แสดงกล่องข้อความ | Show/hide the floating OCR text panel |

---

## 🔧 How It Works

```
Game window
    ↓  Screen Capture API (browser)
Preview in ScreenLingo
    ↓  Draw region over dialog box
Crop selected area
    ↓  Tesseract.js OCR (eng+jpn)
Raw text
    ↓  Noise filter (Thai/English/Japanese line detection)
Clean text
    ↓  Fingerprint dedup (skip if same content)
Display in draggable panel
```

---

## 📝 Notes

- **White text mode** inverts and thresholds the image before OCR — helps with games that have white/colored text on dark backgrounds
- **Frame diff** compares pixel changes before running OCR to save CPU
- **Text fingerprint** uses only Thai characters + English words (4+ letters) for dedup, ignoring UI noise
- Chrome's built-in **Translate Page** feature can be used to translate the detected text

---

## 📜 License

MIT — free to use, modify, and share.
