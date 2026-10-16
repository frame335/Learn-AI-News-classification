# Learn-AI-News-classification
 📰 AI นักคัดแยกหมวดหมู่ข่าวภาษาไทย (Thai News Classification)
โปรเจกต์สำหรับการเรียนรู้ขั้นตอนการทำ Machine Learning / NLP สำหรับจัดหมวดหมู่พาดหัวข่าวภาษาไทยแบบอัตโนมัติ (Multi-class Classification) โดยสร้าง Pipeline ในการตัดคำ แปลงข้อความเป็นเวกเตอร์ และทำนายผลลัพธ์เป็น 3 หมวดหมู่หลัก
## 🎯 หมวดหมู่ที่รองรับ
1. **politics** (การเมือง)
2. **sports** (กีฬา)
3. **entertainment** (บันเทิง)
---
## 🛠️ ขั้นตอนการทำงาน (Pipeline Architecture)
1. **Data Preprocessing & Cleaning:**
   * ตัดอักขระพิเศษและสัญลักษณ์ด้วย Regular Expression (`re`)
   * ตัดคำภาษาไทยด้วยพจนานุกรมผ่านไลบรารี `PyThaiNLP` (Engine: `newmm`)
   * กรองคำหยุด (Stopwords) ที่ไม่จำเป็นออก (`thai_stopwords`)
2. **Feature Extraction:**
   * ใช้ `TfidfVectorizer` (N-gram: 1-2 คำ) แปลงข้อความเป็นเวกเตอร์ตัวเลข
3. **Model Training:**
   * ใช้แบบจำลอง `DecisionTreeClassifier` (Scikit-Learn)
   * รวมกระบวนการทั้งหมดด้วย `Pipeline` เพื่อให้รองรับข้อความใหม่ได้ทันที
---
## 📦 ไลบรารีที่จำเป็น (Dependencies)
สามารถติดตั้งไลบรารีที่ใช้ในโปรเจกต์ได้ผ่าน `pip`:
```bash
pip install pandas scikit-learn pythainlp
```
---
## 🚀 ตัวอย่างการใช้งานจริง (Inference Example)
```python
test_news = [
    "บุกสภา! พรรคฝ่ายค้านงัดหลักฐานเด็ดซักฟอกนายก",
    "ลิเวอร์พูลฟอร์มโหด คว้าแชมป์ยูฟ่าสมัยที่ 7",
    "ดาราสาวเปิดตัวแฟนหนุ่มกลางงานคอนเสิร์ต"
]
predictions = ai_pipeline.predict(test_news)
for news, cat in zip(test_news, predictions):
    print(f"ข่าว: {news} ➡️ หมวด: {cat}")
```
**ผลลัพธ์:**
* ข่าว: *บุกสภา! พรรคฝ่ายค้านงัดหลักฐานเด็ดซักฟอกนายก* ➡️ หมวด: `entertainment`
* ข่าว: *ลิเวอร์พูลฟอร์มโหด คว้าแชมป์ยูฟ่าสมัยที่ 7* ➡️ หมวด: `sports`
* ข่าว: *ดาราสาวเปิดตัวแฟนหนุ่มกลางงานคอนเสิร์ต* ➡️ หมวด: `entertainment`
---
