# /review-examples — วิเคราะห์ Examples ที่จำเป็นสำหรับ Project

สแกน codebase ทั้งหมดแล้ววิเคราะห์ว่ามี pattern อะไรที่ยังขาด example เพื่อให้ `examples/` เป็น SSOT (Single Source of Truth) สำหรับ AI agent

## Process

### Step 1: สแกน Codebase

1. อ่าน `examples/README.md` เพื่อดู example ที่มีอยู่แล้ว
2. สแกนไฟล์ทั้งหมดใน codebase:
   - `apps/` — ทุก app (web, api, และอื่นๆ ที่เพิ่มมา)
   - `libs/` — ทุก shared library
3. อ่านไฟล์หลักๆ ในแต่ละ directory เพื่อระบุ pattern ที่ใช้จริง

### Step 2: ระบุ Pattern ที่ใช้ใน Codebase

วิเคราะห์ code จริงแล้วจัดหมวดหมู่ pattern เช่น:

**Backend patterns:**
- API endpoints / routers
- Services / business logic
- Data models / schemas
- Authentication / authorization
- Database / persistence
- External API integrations
- Background tasks / workers
- Middleware / interceptors
- Error handling patterns
- Testing patterns

**Frontend patterns:**
- Components (page, layout, UI)
- State management (context, store, hooks)
- API calls / data fetching
- Routing / navigation
- Form handling / validation
- Styling patterns
- Testing patterns

**Shared patterns:**
- Type definitions / interfaces
- Utility functions
- Constants / config

### Step 3: เปรียบเทียบกับ Examples ที่มี

สร้างตารางเปรียบเทียบ:

| Pattern | มี Example แล้ว? | ไฟล์ต้นฉบับใน Codebase | ความสำคัญ |
|---------|------------------|------------------------|-----------|

**เกณฑ์ความสำคัญ:**
- **สูง (High):** Pattern ที่ใช้บ่อยหรือซับซ้อน — AI agent จะต้องทำซ้ำแน่นอน
- **กลาง (Medium):** Pattern ที่ใช้เป็นครั้งคราว — มี example จะช่วยลด error
- **ต่ำ (Low):** Pattern ที่ใช้น้อยหรือตรงไปตรงมา — ไม่จำเป็นต้องมี example

### Step 4: ตรวจสอบ Example ที่มีอยู่

สำหรับ example ที่มีอยู่แล้ว ตรวจสอบว่า:
- ยังตรงกับ code จริงหรือไม่ (ต้นฉบับอาจเปลี่ยนไปแล้ว)
- มี annotations ครบหรือไม่ (`# PATTERN:`, `# GOTCHA:`, `# CRITICAL:`)
- ครอบคลุม pattern สำคัญทั้งหมดหรือไม่

### Step 5: รายงานผลให้ User

แสดงผลลัพธ์เป็น 3 ส่วน:

**1. Examples ที่ควรสร้างใหม่ (เรียงตามความสำคัญ)**
- ระบุ pattern, ไฟล์ต้นฉบับ, เหตุผลว่าทำไมถึงจำเป็น

**2. Examples ที่ต้องอัพเดท (ถ้ามี)**
- ระบุว่าอะไรเปลี่ยนไปจากต้นฉบับ

**3. Examples ที่ครบถ้วนแล้ว**
- ยืนยันว่า example ยังถูกต้องและตรงกับ code จริง

### Step 6: ถาม User

ใช้ AskUserQuestion ถาม user ว่าต้องการให้:
- สร้าง example ใหม่ตัวไหนบ้าง
- อัพเดท example ตัวไหนบ้าง
- หรือเสร็จสิ้นแค่รายงาน

### Step 7: ดำเนินการ (ถ้า User ต้องการ)

สำหรับแต่ละ example ที่ user เลือก:
1. อ่าน code ต้นฉบับจริงจาก codebase
2. คัดลอกมาเป็น example พร้อมเพิ่ม annotations:
   - `# PATTERN:` — อธิบาย pattern ที่ใช้
   - `# GOTCHA:` — สิ่งที่ต้องระวัง
   - `# CRITICAL:` — สิ่งที่ห้ามพลาด
3. บันทึกไฟล์ใน `examples/` ตาม directory structure ที่เหมาะสม
4. อัพเดท `examples/README.md` — เพิ่มในตาราง ดัชนี Pattern และโครงสร้าง
5. อัพเดท `CLAUDE.md` section "Examples Reference" ให้ตรงกัน

## Rules

- **คัดลอกจาก code จริงเท่านั้น** — ห้ามเขียน example จากจินตนาการ
- **ไม่สร้าง example ซ้ำ** — ถ้ามีอยู่แล้วและยังถูกต้อง ให้ข้ามไป
- **Annotations เป็นภาษาไทย** — ตาม coding convention ของโปรเจค
- **ไม่แก้ code ต้นฉบับ** — skill นี้แค่อ่านและสร้าง example เท่านั้น
