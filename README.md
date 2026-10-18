# Vue Gold Price API

งานแบบฝึกหัด Vue.js: โปรแกรมคำนวณเกรดและดึงราคาทองคำจาก API มาแสดงผล ใช้ Vue 3, Vite และ Bootstrap 5

## วิธีรัน

```bash
npm install
npm run dev
```

เปิด URL ที่ Terminal แสดง (โดยทั่วไปคือ http://localhost:5173)

## ฟังก์ชัน
- หน้าราคาทองคำ ดึงข้อมูลจริงจาก `https://api.gold-api.com/price/XAU` ด้วย `fetch()` เมื่อเปิดหน้าเว็บ มีปุ่มโหลดใหม่และโหลดอัตโนมัติทุก 60 วินาที
- หน้าคำนวณเกรด: A 80+, B+ 75+, B 70+, C+ 65+, C 60+, D+ 55+, D 50+, F ต่ำกว่า 50
- การแสดงผลด้วย Vue.js + Bootstrap

**ข้อควรทราบ:** ราคาที่ API ส่งกลับเป็นราคาทองคำ Spot ในสกุล USD/ทรอยออนซ์ ไม่ใช่ราคาทองแท่งไทย 96.5% และไม่ใช่ราคาซื้อขายของโบรกเกอร์รายใดรายหนึ่ง

## ส่งงาน
1. แคปหน้าจอเว็บหน้าราคาทองคำและหน้าคำนวณเกรด
2. แคปผล JSON ที่ URL API
3. Push โปรเจกต์นี้ขึ้น GitHub แล้วแนบลิงก์ Repository

## GitHub
สร้าง Repository ชื่อ `Vue-Gold-Price-API` เป็น Public (ไม่ต้องเพิ่ม README หรือ .gitignore ผ่านหน้า GitHub เพราะมีในโปรเจกต์แล้ว) แล้วจากโฟลเดอร์นี้รัน:

```bash
git init
git add .
git commit -m "Vue grade calculator and gold API"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/Vue-Gold-Price-API.git
git push -u origin main
```

เปลี่ยน `YOUR_USERNAME` เป็น GitHub username ของคุณ
