# /generate-project-structure — สร้าง PROJECT_STRUCTURE.md สำหรับเป็น Base ในการ Coding

วิเคราะห์โปรเจคแล้วสร้างไฟล์ `PROJECT_STRUCTURE.md` ที่เป็น Source of Truth สำหรับโครงสร้างโปรเจค — AI agent ต้องยึดไฟล์นี้ในการสร้าง/จัดวางไฟล์ทุกครั้ง

## Process

### Step 1: ตรวจสอบสถานะโปรเจค

ตรวจว่าโปรเจคมี source code อยู่แล้วหรือยัง:

1. สแกน root directory ดูไฟล์ config (เช่น `package.json`, `pyproject.toml`, `go.mod`)
2. สแกนดู directory หลัก (เช่น `apps/`, `libs/`, `src/`, `cmd/`)
3. ตรวจดูว่า `CLAUDE.md` กรอกข้อมูลจริงแล้วหรือยังเป็น template

**ถ้ามี source code → ไป Step 3 (Auto-detect)**
**ถ้ายังไม่มี source code → ไป Step 2 (Interview)**

### Step 2: Interview — ถามข้อมูลจาก User

ใช้ AskUserQuestion ถามทีละกลุ่ม:

**กลุ่มที่ 1 — พื้นฐาน:**

1. **ชื่อโปรเจค:** โปรเจคนี้ชื่ออะไร?
2. **Programming Language:** ใช้ภาษาอะไร? (TypeScript / Python / Go / Java / Rust / อื่น ๆ)
3. **Framework:** ใช้ framework อะไร? (Next.js / FastAPI / Express / NestJS / Gin / Spring Boot / อื่น ๆ)
4. **ประเภทโปรเจค:** เป็นแบบไหน?
   - `REST API` — backend API อย่างเดียว
   - `Full-stack web app` — frontend + backend
   - `CLI tool` — command line application
   - `Library/Package` — shared library สำหรับ publish
   - `Monorepo` — หลาย apps/packages
   - `อื่น ๆ` — ให้ user อธิบาย

**กลุ่มที่ 2 — Stack เพิ่มเติม (ถามเฉพาะที่เกี่ยวข้อง):**

5. **Database:** ใช้ database อะไร? (PostgreSQL / MongoDB / SQLite / Redis / ไม่มี)
6. **ORM / Query Builder:** ใช้อะไร? (Prisma / Drizzle / SQLAlchemy / TypeORM / ไม่มี)
7. **Auth:** ต้องการระบบ authentication ไหม? (NextAuth / Clerk / Passport / custom / ไม่มี)
8. **Testing:** ใช้ test framework อะไร? (Vitest / Jest / Pytest / Go testing)
9. **State Management (ถ้าเป็น frontend):** ใช้อะไร? (Zustand / Redux / Jotai / React Context / ไม่มี)

**กลุ่มที่ 3 — โครงสร้าง (ถามถ้าเป็น Monorepo หรือโปรเจคใหญ่):**

10. **มีกี่ apps?** ชื่ออะไรบ้าง? หน้าที่ของแต่ละ app?
11. **มี shared libraries ไหม?** ชื่ออะไร? ใช้ทำอะไร?
12. **มี pattern เฉพาะที่อยากใช้ไหม?** (เช่น DDD, Clean Architecture, Hexagonal)

หลังได้คำตอบครบ → ไป Step 4

### Step 3: Auto-detect — วิเคราะห์จาก Codebase ที่มี

1. อ่าน config files เพื่อระบุ stack:
   - `package.json` → dependencies, scripts, workspaces
   - `pyproject.toml` → Python dependencies, build system
   - `go.mod` → Go modules
   - `tsconfig.json` → TypeScript configuration
2. สแกน directory structure ทั้งหมด:
   - ใช้ Glob เพื่อดูโครงสร้าง directory
   - ระบุ pattern ที่ใช้ (เช่น route-based, feature-based, layer-based)
3. อ่านไฟล์หลักในแต่ละ directory เพื่อเข้าใจหน้าที่
4. ตรวจ `CLAUDE.md` ว่ามีข้อมูล structure อยู่แล้วหรือไม่

### Step 4: Research Best Practices

ค้นหา best practices สำหรับ stack ที่ระบุ:

1. **ค้นหาด้วย WebSearch:**
   - "{framework} recommended project structure {year}"
   - "{language} {project-type} directory structure best practices"
   - ถ้าเป็น monorepo: "{monorepo-tool} workspace structure guide"

2. **สิ่งที่ต้องตรวจสอบ:**
   - Official documentation ของ framework แนะนำ structure แบบไหน
   - Community conventions ที่เป็นที่ยอมรับ
   - Scalability — structure รองรับการเติบโตหรือไม่
   - Separation of concerns — แยก layer ชัดเจนหรือไม่

### Step 5: นำเสนอ Plan ให้ User

แสดงโครงสร้างที่จะสร้างให้ user เห็น:

1. **แสดง tree structure** แบบ annotated — มี comment อธิบายหน้าที่ทุก directory
2. **แสดงเหตุผล** ว่าทำไมถึงเลือก structure นี้
3. **แสดง best practices** ที่พบจาก research
4. **แสดง trade-offs** (ข้อดี/ข้อเสีย)

ถาม user: "ต้องการปรับอะไรไหม?" → ถ้ามีก็ปรับ plan ก่อนสร้าง

### Step 6: สร้าง PROJECT_STRUCTURE.md

**ตำแหน่งของไฟล์ขึ้นอยู่กับประเภทโปรเจค:**

| โครงสร้างโปรเจค | ตำแหน่ง | เหตุผล |
|----------------|---------|--------|
| **Single app** | `PROJECT_STRUCTURE.md` ที่ root | ไฟล์เดียวครอบคลุมทั้งโปรเจค |
| **Monorepo** | `apps/{app-name}/PROJECT_STRUCTURE.md` ต่อแต่ละ app | แต่ละ app มี structure เป็นของตัวเอง กันสับสนข้าม app |

**สำหรับ Monorepo:**
- สร้าง `PROJECT_STRUCTURE.md` แยกในแต่ละ app — ห้ามใช้ไฟล์เดียวรวมทุก app
- Root level อาจมี `PROJECT_STRUCTURE.md` สำหรับ shared structure (เช่น `libs/`, `infra/`, `packages/`) แยกต่างหาก
- แต่ละไฟล์ต้องระบุ scope ชัดเจนว่าครอบคลุม directory ไหน

สร้างไฟล์ตามโครงสร้างดังนี้:

```markdown
# PROJECT_STRUCTURE.md — {ชื่อโปรเจค}

> ไฟล์นี้เป็น **Source of Truth** สำหรับโครงสร้างโปรเจค
> AI agent ต้องยึดโครงสร้างนี้ในการสร้าง/จัดวางไฟล์ทุกครั้ง

## Directory Structure

{tree structure แบบ annotated}

## Directory Descriptions

{อธิบายหน้าที่ของแต่ละ directory สำคัญ}

## File Naming Conventions

{กฎการตั้งชื่อไฟล์ในแต่ละ directory}

## Rules

{กฎที่ต้องปฏิบัติตามเมื่อสร้าง/จัดวางไฟล์}
```

**รายละเอียดแต่ละ section:**

**Directory Structure:**
- ใช้ tree format พร้อม comment อธิบายทุก directory
- แสดงตัวอย่างไฟล์ที่ควรอยู่ในแต่ละ directory
- ใช้ `{placeholder}` สำหรับชื่อที่เปลี่ยนได้

**Directory Descriptions:**
- อธิบายหน้าที่ของแต่ละ directory สำคัญ
- ระบุว่าไฟล์ประเภทไหนควรอยู่ที่ไหน
- ระบุ pattern ที่ใช้ (เช่น "1 file ต่อ 1 route", "barrel export ด้วย index.ts")

**File Naming Conventions:**
- กฎการตั้งชื่อไฟล์ในแต่ละ directory
- เช่น components ใช้ PascalCase, services ใช้ camelCase, Python modules ใช้ snake_case

**Rules:**
- ห้ามสร้างไฟล์/directory นอก structure ที่กำหนด
- ถ้าต้องเพิ่ม directory ใหม่ ต้องอัพเดท PROJECT_STRUCTURE.md ก่อน
- ไฟล์ต้องอยู่ใน directory ที่ตรงกับหน้าที่

### Step 7: อัพเดท CLAUDE.md

อัพเดท Section 4 (Project Structure) ใน `CLAUDE.md`:

1. เพิ่มข้อความว่าให้ยึด `PROJECT_STRUCTURE.md` เป็นหลัก
2. คัดลอก tree structure มาแสดงเป็น overview
3. ลบ placeholder/TODO ที่เติมแล้วออก

### Step 8: รายงานผล

แสดงสรุป:
- โครงสร้างที่สร้าง
- Best practices ที่นำมาใช้
- กฎสำคัญที่ AI agent ต้องปฏิบัติตาม
- สิ่งที่ user อาจต้องปรับเพิ่มในอนาคต

## Rules

- **ค้นหา best practices เสมอ** — ห้ามสร้าง structure จากจินตนาการอย่างเดียว ต้อง research ก่อน
- **ถาม user ก่อนสร้าง** — แสดง plan ให้ user approve ก่อนเขียนไฟล์
- **Annotate ทุก directory** — ทุก directory ต้องมี comment อธิบายหน้าที่
- **ยึด official convention ของ framework** — ถ้า framework มี recommended structure ให้ใช้เป็นฐาน
- **ห้ามลบ/overwrite** `PROJECT_STRUCTURE.md` ที่มีอยู่แล้วโดยไม่ถาม user ก่อน
- **Sync กับ CLAUDE.md** — อัพเดท Section 4 ให้ตรงกับ `PROJECT_STRUCTURE.md` เสมอ
