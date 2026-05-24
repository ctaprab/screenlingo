# 🎮 ScreenLingo v2.1

**ScreenLingo** คือเครื่องมืออ่านข้อความในเกมแบบอัตโนมัติ ทำงานบน Browser ไม่ต้องติดตั้งโปรแกรมใดๆ ใช้ OCR อ่านข้อความจากหน้าจอเกมและแสดงผลในกล่องข้อความที่ยึดซ้าย/ขวาหรือลากวางได้ พร้อม Popup ลอยเหนือเกมเสมอ

> **ScreenLingo** is a browser-based live OCR overlay for gamers — no installation needed. Captures your game window, reads on-screen dialog text automatically (optimised for pixel-art fonts), and displays it in a dockable panel and an always-on-top popup window.

---

## ✨ คุณสมบัติ v2.1 / Features

| คุณสมบัติ | รายละเอียด |
|-----------|------------|
| 📺 จับภาพหน้าจอ | Screen Capture API — จับหน้าต่างเกมโดยตรง |
| ✏️ กำหนดพื้นที่ OCR | ลากเพื่อเลือกเฉพาะบริเวณกล่องบทสนทนา |
| 🔍 Pixel-font upscale | ขยายภาพ 1–6× ด้วย nearest-neighbor (ไม่เบลอ) ก่อนส่ง OCR |
| 🎯 Otsu's threshold | คำนวณจุดตัดขาว/ดำที่เหมาะสมอัตโนมัติจาก histogram ของภาพ |
| 🔄 สแกนอัตโนมัติ | สแกนซ้ำทุก 2–15 วินาที ข้ามข้อความซ้ำด้วย Text Fingerprint |
| ⬜ โหมดข้อความสีขาว | กลับสีก่อน threshold เหมาะกับ UI เกมที่ตัวอักษรสีขาวบนพื้นมืด |
| 📖 กล่องข้อความ | ลากวาง, ปรับขนาด, หรือยึดชิดซ้าย/ขวา (snap) |
| 🪟 Popup อยู่บนสุด | Document Picture-in-Picture API — ลอยเหนือทุกหน้าต่าง |
| 🇹🇭🇬🇧🇯🇵 รองรับหลายภาษา | Tesseract.js OCR — English, Japanese (PSM 6: single text block) |

---

## 📁 ไฟล์ในโปรเจกต์ / Project Files

```
screenlingo/
├── index.html                ← หน้าเริ่มต้น (redirect ไป screenlingo-simple.html)
├── screenlingo-simple.html   ← แอปหลัก (Main App)
├── screenlingo-popup.html    ← Popup สำรอง (Browser ที่ไม่รองรับ Document PiP)
└── README.md
```

---

## 🚀 วิธีใช้งาน / How to Use

### เปิดด้วย Chrome หรือ Edge

เปิดไฟล์ `index.html` ด้วย Google Chrome หรือ Microsoft Edge ตรงๆ ได้เลย  
(ต้องใช้ Chrome/Edge 116+ เพื่อรองรับ Document Picture-in-Picture)

> หากพบปัญหา CORS ให้เปิด Chrome ด้วย flag:
> ```
> chrome.exe --disable-web-security --user-data-dir="C:\ChromeDev" --allow-file-access-from-files
> ```

### ขั้นตอนการใช้งาน

```
1. คลิก [📺 จับภาพหน้าจอ]
   → เลือกหน้าต่างเกม (แนะนำ "Window" แทน "Entire Screen")

2. คลิก [✏️ กำหนดพื้นที่]
   → ลากครอบกล่องบทสนทนาในเกม — ครอบให้แน่น ยิ่งแม่นยำ

3. [⬜ ข้อความสีขาว] ในกล่องข้อความ
   → เปิด : ตัวอักษรสีขาวบนพื้นมืด (ค่าเริ่มต้น)
   → ปิด  : ตัวอักษรสีดำบนพื้นสว่าง

4. Slider [ขยาย Nx]
   → เพิ่มค่าเป็น 3–4× สำหรับ pixel font เล็กๆ (8–12px)
   → Tesseract อ่านได้แม่นยำขึ้นมากเมื่อตัวอักษรใหญ่พอ

5. คลิก [▶ เริ่มสแกน]
   → ข้อความใหม่ปรากฏในกล่องอัตโนมัติ ข้อความซ้ำถูกข้ามทันที

6. [◀] หรือ [▶] ในหัวกล่องข้อความ
   → ยึดกล่องชิดซ้ายหรือขวาของหน้าจอ (คลิกซ้ำเพื่อปลดล็อก)

7. คลิก [🪟 เปิดป็อปอัปบนสุด]
   → กล่องข้อความลอยเหนือเกม ปรับสีพื้นหลังและขนาด font ได้
```

---

## ⚙️ การตั้งค่า / Settings

| การตั้งค่า | รายละเอียด | ค่าเริ่มต้น |
|-----------|------------|-------------|
| **ทุก N วินาที** | ความถี่การสแกน | 3 วินาที |
| **ขยาย Nx** | อัตราการขยายภาพก่อน OCR (1–6×) | 3× |
| **⬜ ข้อความสีขาว** | กลับสีก่อน threshold | เปิด |
| **ขนาดตัวอักษร** | ขนาด Font ในกล่องข้อความ | 20px |

---

## 🔧 หลักการทำงาน v2.1 / How It Works

```
หน้าจอเกม
    ↓  Screen Capture API
Preview ใน ScreenLingo
    ↓  ลากเลือกพื้นที่ Dialog Box
Crop Region
    ↓  Frame diff (ข้ามถ้าไม่มีการเปลี่ยนแปลง)
    ↓  Upscale ×N ด้วย nearest-neighbor (ไม่เบลอ pixel)
    ↓  Grayscale → Otsu's threshold → Pure B&W
Preprocessed Image
    ↓  Tesseract.js OCR (eng+jpn, PSM 6)
Raw Text
    ↓  Noise filter (ข้ามบรรทัดที่มีสัญลักษณ์/อักขระน้อยเกินไป)
Clean Text
    ↓  Text Fingerprint Dedup (ข้ามถ้าซ้ำ)
แสดงในกล่องข้อความ + Popup (BroadcastChannel)
```

**ทำไม Otsu's threshold ดีกว่า hardcode 128?**  
Otsu คำนวณจุดตัดที่ลด within-class variance สูงสุด — ทำงานได้กับภาพที่มีคอนทราสต์ต่างกันโดยไม่ต้องปรับด้วยมือ

**ทำไมต้อง nearest-neighbor ไม่ใช่ bilinear?**  
Pixel font ใช้พิกเซลแบบ hard edge — bilinear จะเบลอขอบทำให้ Tesseract สับสน nearest-neighbor รักษาขอบคมไว้

---

## 🖥️ ความต้องการของระบบ / Requirements

| รายการ | รายละเอียด |
|--------|------------|
| **Browser** | Google Chrome 116+ หรือ Microsoft Edge 116+ |
| **OS** | Windows 10/11, macOS, Linux |
| **Internet** | ครั้งแรกเท่านั้น — โหลด Tesseract OCR pack (~10 MB) |
| **API Key** | ไม่ต้องการ — ฟรี 100% |

---

## ❓ FAQ

**Q: OCR อ่านผิดหรืออ่านไม่ออก?**
- เพิ่ม Slider **ขยาย** เป็น 4–5× (สำหรับ pixel font 8–10px)
- ลากพื้นที่ใหม่ให้แน่นขึ้น — ครอบเฉพาะกล่องข้อความ ไม่ใช่ทั้งหน้าจอ
- ตรวจสอบว่า **⬜ ข้อความสีขาว** ตั้งถูกต้องตามสีตัวอักษรในเกม

**Q: ปุ่ม 🪟 Popup ใช้ไม่ได้?**  
ต้องใช้ Chrome หรือ Edge 116+ เท่านั้น หากไม่รองรับ เปิด `screenlingo-popup.html` เป็นหน้าต่างแยกแทน

**Q: ข้อความไม่อัปเดต?**  
ลดเวลา interval หรือลากกำหนดพื้นที่ใหม่

**Q: ใช้กับเกมอะไรได้บ้าง?**  
ทุกเกมที่แสดงข้อความบทสนทนาบนหน้าจอ — JRPG, Visual Novel, MMO, Story games

---

## 🙏 Credits

- [Tesseract.js](https://github.com/naptha/tesseract.js) — OCR Engine
- [Google Fonts — Sarabun](https://fonts.google.com/specimen/Sarabun) — Thai UI Font
- [Document Picture-in-Picture API](https://developer.chrome.com/docs/web-platform/document-picture-in-picture/) — Always on Top Window

---

## 📜 License

MIT License — ใช้งาน แก้ไข และแจกจ่ายได้ฟรี
