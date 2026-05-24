# 🎮 ScreenLingo

**ScreenLingo** คือเครื่องมืออ่านข้อความในเกมแบบอัตโนมัติ ทำงานบน Browser ไม่ต้องติดตั้งโปรแกรมใด ๆ ใช้ OCR อ่านข้อความจากหน้าจอเกม แล้วแสดงผลในกล่องข้อความที่ลากวางได้ และ popup อยู่บนสุดเสมอ (Always on Top)

> **ScreenLingo** is a browser-based live OCR overlay for gamers. No installation required. Captures your game window, reads on-screen text automatically, and displays it in a draggable panel and an always-on-top popup window.

---

## ✨ คุณสมบัติ / Features

| คุณสมบัติ | รายละเอียด |
|-----------|------------|
| 📺 จับภาพหน้าจอ | ใช้ Screen Capture API จับภาพหน้าต่างเกมโดยตรง |
| ✏️ กำหนดพื้นที่ OCR | ลากเพื่อเลือกบริเวณที่มีข้อความบทสนทนา |
| 🔄 สแกนอัตโนมัติ | สแกนซ้ำทุก N วินาที ตรวจจับการเปลี่ยนแปลงด้วย Frame Diff |
| 🧹 กรองสัญญาณรบกวน | ตัดข้อความ UI, สัญลักษณ์, และตัวอักษรสั้น ๆ ออกอัตโนมัติ |
| ⬜ โหมดข้อความสีขาว | ปรับภาพก่อน OCR สำหรับตัวอักษรสีขาวบนพื้นหลังมืด |
| 📖 กล่องข้อความลากได้ | กล่องข้อความลอยอยู่เหนือ Preview ลากวางและปรับขนาดได้ |
| 🪟 Popup อยู่บนสุด | ใช้ Document Picture-in-Picture API สร้างหน้าต่างลอยเหนือทุกอย่าง |
| 🌐 แปลภาษาด้วย Chrome | คลิกขวา → แปลภาษา บนหน้าหลัก ข้อความแปลแล้วจะซิงค์ไปยัง Popup อัตโนมัติ |
| 🇹🇭🇬🇧🇯🇵 รองรับหลายภาษา | OCR รองรับ ภาษาอังกฤษ, ไทย และญี่ปุ่น |
| 🔁 ข้ามข้อความซ้ำ | ใช้ Fingerprint เปรียบเทียบเนื้อหาจริง ไม่ใช่ Pixel เพื่อข้ามข้อความซ้ำ |

---

## 📁 ไฟล์ในโปรเจกต์ / Project Files

```
screenlingo/
├── screenlingo-simple.html   ← แอปหลัก (Main App)
├── screenlingo-popup.html    ← ป็อปอัปแบบแยกไฟล์ (Standalone Popup)
└── README.md                 ← ไฟล์นี้
```

> **หมายเหตุ:** `screenlingo-popup.html` ใช้สำหรับกรณีที่เบราว์เซอร์ไม่รองรับ Document Picture-in-Picture  
> หากใช้ Chrome 116+ ให้ใช้ปุ่ม **🪟 เปิดป็อปอัปบนสุด** ใน `screenlingo-simple.html` แทน

---

## 🚀 วิธีติดตั้งและใช้งาน / How to Use

### ขั้นตอนที่ 1 — เปิดด้วย Chrome (จำเป็น)

เนื่องจากแอปนี้ต้องเข้าถึงไฟล์ในเครื่อง ต้องเปิด Chrome ด้วยคำสั่งพิเศษ:

```cmd
"C:\Program Files\Google\Chrome\Application\chrome.exe" --disable-web-security --user-data-dir="C:\ChromeDev" --allow-file-access-from-files "C:\Users\ชื่อผู้ใช้\Downloads\screenlingo-simple.html"
```

> 💡 แทน `ชื่อผู้ใช้` ด้วยชื่อ User Windows ของคุณ เช่น `bom`

---

### ขั้นตอนที่ 2 — ใช้งานในแอป

```
1. คลิก [📺 จับภาพหน้าจอ]
   → เลือกหน้าต่างเกมที่ต้องการอ่านข้อความ

2. คลิก [✏️ กำหนดพื้นที่]
   → ลากครอบบริเวณกล่องบทสนทนาในเกม (dialog box)
   → ยิ่งครอบแน่น ยิ่งแม่นยำ

3. คลิก [▶ เริ่มสแกน]
   → แอปจะอ่านข้อความอัตโนมัติทุก 3 วินาที
   → ข้อความใหม่จะปรากฏในกล่องข้อความด้านล่าง

4. แปลภาษา (ไม่บังคับ)
   → คลิกขวาที่หน้าจอหลัก → "แปลเป็นภาษาไทย"
   → ข้อความที่แปลแล้วจะซิงค์ไปยัง Popup อัตโนมัติ

5. คลิก [🪟 เปิดป็อปอัปบนสุด]
   → เปิดหน้าต่างลอยเหนือเกม (Always on Top)
   → ลากวางตำแหน่งได้ตามต้องการ
   → กดปุ่ม 🌑 เพื่อเปลี่ยนธีมสีพื้นหลัง
```

---

## ⚙️ การตั้งค่า / Settings

| การตั้งค่า | รายละเอียด |
|-----------|------------|
| **ทุก N วินาที** | ความถี่ในการสแกน (2–15 วินาที) |
| **⬜ ข้อความสีขาว: เปิด/ปิด** | เปิดใช้เมื่อตัวอักษรในเกมเป็นสีขาวบนพื้นหลังมืด |
| **ขนาดตัวอักษร** | ปรับขนาดตัวอักษรในกล่องข้อความและ Popup |
| **📖 แสดงกล่องข้อความ** | แสดงกล่องข้อความที่ซ่อนอยู่ |
| **🪟 เปิดป็อปอัปบนสุด** | เปิดหน้าต่าง Always on Top (ต้องใช้ Chrome 116+) |

---

## 🔧 หลักการทำงาน / How It Works

```
หน้าจอเกม (Game Window)
        ↓  Screen Capture API
Preview ใน ScreenLingo
        ↓  ลากเลือกพื้นที่ Dialog Box
ตัดภาพเฉพาะส่วน (Crop Region)
        ↓  Frame Diff (เปรียบเทียบ Pixel)
     มีการเปลี่ยนแปลง?
        ↓  ใช่ → Tesseract.js OCR (eng+jpn)
ข้อความดิบ (Raw Text)
        ↓  กรองสัญญาณรบกวน (Noise Filter)
ข้อความสะอาด (Clean Text)
        ↓  Fingerprint Dedup (ข้ามถ้าซ้ำ)
แสดงในกล่องข้อความหลัก
        ↓  Chrome Translate (คลิกขวา)
ข้อความแปลแล้ว
        ↓  MutationObserver + BroadcastChannel
แสดงใน Popup Always on Top
```

---

## 🖥️ ความต้องการของระบบ / Requirements

| รายการ | รายละเอียด |
|--------|------------|
| **Browser** | Google Chrome 116+ หรือ Microsoft Edge 116+ |
| **OS** | Windows 10/11 (แนะนำ), macOS, Linux |
| **Internet** | ต้องการเชื่อมต่อครั้งแรกสำหรับดาวน์โหลด OCR Language Pack |
| **API Key** | ไม่ต้องการ — ฟรี 100% |
| **Installation** | ไม่ต้องติดตั้ง — เปิดไฟล์ HTML ได้เลย |

---

## ❓ คำถามที่พบบ่อย / FAQ

**Q: ทำไมต้องเปิด Chrome ด้วย `--disable-web-security`?**  
A: เพราะแอปต้องโหลด Tesseract.js จาก CDN และเข้าถึงไฟล์ในเครื่อง ซึ่งถูกบล็อกโดยนโยบาย CORS ของ Browser ปกติ

**Q: ปุ่ม 🪟 เปิดป็อปอัปบนสุด ใช้ไม่ได้?**  
A: ต้องใช้ Chrome หรือ Edge เวอร์ชัน 116 ขึ้นไป และต้องเปิดด้วย Flag ที่กำหนดข้างต้น

**Q: OCR อ่านผิดหรืออ่านได้ไม่ครบ?**  
A: ลองปรับพื้นที่ให้ครอบแน่นขึ้น และเปิด **โหมดข้อความสีขาว** หากตัวอักษรในเกมเป็นสีอ่อนบนพื้นหลังมืด

**Q: Popup แสดงข้อความภาษาอังกฤษ ไม่ใช่ไทย?**  
A: ต้องแปลหน้าหลักก่อนโดยคลิกขวา → แปลภาษา จากนั้น Popup จะซิงค์ข้อความที่แปลแล้วอัตโนมัติ

**Q: ใช้กับเกมอะไรได้บ้าง?**  
A: ใช้ได้กับเกมทุกประเภทที่มีข้อความบทสนทนาบนหน้าจอ เช่น JRPG, Visual Novel, MMO, และเกมแนว Story-driven

---

## 📝 หมายเหตุ / Notes

- **โหมดข้อความสีขาว** จะ Invert + Threshold ภาพก่อนส่งให้ OCR เหมาะกับเกมที่ตัวอักษรสีขาวบนพื้นหลังมืด
- **Frame Diff** เปรียบเทียบ Pixel ก่อนรัน OCR เพื่อประหยัด CPU — OCR จะทำงานเฉพาะเมื่อหน้าจอเปลี่ยน
- **Text Fingerprint** ใช้ตัวอักษรไทย + ญี่ปุ่น + คำภาษาอังกฤษ (4+ ตัว) เพื่อเปรียบเทียบว่าข้อความซ้ำหรือไม่
- **MutationObserver** คอยตรวจจับการเปลี่ยนแปลงของ DOM เมื่อ Chrome แปลหน้า แล้วส่งข้อความที่แปลแล้วไปยัง Popup

---

## 📜 License

MIT License — ใช้งาน แก้ไข และแจกจ่ายได้ฟรี

---

## 🙏 Credits

- [Tesseract.js](https://github.com/naptha/tesseract.js) — OCR Engine
- [Google Fonts — Sarabun](https://fonts.google.com/specimen/Sarabun) — Thai Font
- [Document Picture-in-Picture API](https://developer.chrome.com/docs/web-platform/document-picture-in-picture/) — Always on Top Window
