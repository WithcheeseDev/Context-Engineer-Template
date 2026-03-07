# /review-examples — วิเคราะห์ Examples ที่จำเป็นสำหรับ Project

สแกน codebase ทั้งหมดแล้ววิเคราะห์ว่ามี pattern อะไรที่ยังขาด example เพื่อให้ `examples/` เป็น SSOT (Single Source of Truth) สำหรับ AI agent

## Process

### Step 0: ตรวจสอบสถานะโปรเจค

ก่อนเริ่มสแกน ให้ตรวจสอบว่าโปรเจคมี source code จริงหรือยัง:

1. ตรวจดูว่ามีไฟล์ source code ใน `apps/`, `libs/`, `src/` หรือ directory หลักหรือไม่
2. ตรวจดูว่า `CLAUDE.md` ยังเป็น template (มี placeholder `{...}` อยู่) หรือกรอกข้อมูลจริงแล้ว

**ถ้าโปรเจคยังไม่ได้ตั้งค่า / ยังไม่มี source code:**

ใช้ AskUserQuestion ถามข้อมูลต่อไปนี้ทีละข้อจนครบ:

1. **Programming Language:** ใช้ภาษาอะไร? (เช่น TypeScript, Python, Go, Java, Rust)
2. **Framework:** ใช้ framework อะไร? (เช่น Next.js, FastAPI, Express, NestJS, Gin, Spring Boot)
3. **ประเภทโปรเจค:** เป็นแบบไหน? (เช่น REST API, Full-stack web app, CLI tool, Monorepo)
4. **Database:** ใช้ database อะไร? (เช่น PostgreSQL, MongoDB, SQLite, ไม่มี)
5. **ORM / Query Builder:** ใช้อะไร? (เช่น Prisma, Drizzle, SQLAlchemy, TypeORM, ไม่มี)
6. **Testing framework:** ใช้อะไร? (เช่น Vitest, Jest, Pytest, Go testing)
7. **Pattern เพิ่มเติม:** มี pattern เฉพาะที่อยากได้ example ไหม? (เช่น Authentication, WebSocket, Background jobs, File upload)

หลังได้ข้อมูลครบแล้ว:

1. ใช้ WebSearch ค้นหา best practice examples สำหรับ stack ที่ user เลือก
2. รวบรวม example patterns ที่เป็น best practice ของ stack นั้น เช่น:
   - Project structure ที่แนะนำ
   - API endpoint pattern (routing, validation, error handling)
   - Service layer / business logic pattern
   - Database / repository pattern
   - Testing pattern (unit test, integration test)
   - Authentication / authorization pattern
   - Error handling pattern
3. นำเสนอ example patterns ที่พบให้ user เลือกว่าต้องการสร้างตัวไหน
4. สร้าง example files ใน `examples/` พร้อม annotations ตาม convention
5. อัพเดท `examples/README.md` และ `CLAUDE.md` section "Examples Reference"

**ถ้าโปรเจคมี source code แล้ว → ไปต่อ Step 1**

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
