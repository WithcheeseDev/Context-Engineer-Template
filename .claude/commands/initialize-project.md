# /initialize-project — Initialize Project Structure & Configuration

ตั้งค่าโปรเจคใหม่ตั้งแต่ต้น — สร้างโครงสร้าง, ติดตั้ง dependencies, กำหนด config, และอัพเดท CLAUDE.md ให้ตรงกับโปรเจคจริง

## Process

### Phase 1: Gather Requirements (ถาม User)

ถาม user ทีละกลุ่ม ใช้ AskUserQuestion — **ห้ามข้ามขั้นตอนนี้**

**กลุ่มที่ 1 — Core Decisions:**

1. **Project Structure:** โปรเจคจะใช้โครงสร้างแบบไหน?
   - `monolib` — single app, shared folders ภายใน (เหมาะกับโปรเจคขนาดเล็ก-กลาง)
   - `monorepo (Nx)` — หลาย apps/libs แยก workspace (เหมาะกับโปรเจคขนาดใหญ่, หลายทีม)
   - `monorepo (Turborepo)` — หลาย apps/packages ใช้ Turborepo
   - `monorepo (pnpm workspaces)` — หลาย packages จัดการด้วย pnpm
   - `อื่น ๆ` — ให้ user อธิบาย

2. **Programming Language:** ภาษาหลักที่ใช้?
   - TypeScript / JavaScript / Python / Go / Rust / อื่น ๆ

3. **Tech Stack หลัก:**
   - Web Framework (เช่น Next.js, FastAPI, Express, Gin)
   - Database (เช่น PostgreSQL, MongoDB, Redis, SQLite, ไม่มี)
   - ORM/Query Builder (เช่น Prisma, Drizzle, SQLAlchemy, ไม่มี)

**กลุ่มที่ 2 — ประเมินคำตอบแล้วถาม Follow-up:**

วิเคราะห์คำตอบจากกลุ่มที่ 1 แล้วถามคำถามเพิ่มเติมที่จำเป็น เช่น:

- ถ้าเลือก **monorepo** → ถามว่ามีกี่ apps? ชื่ออะไรบ้าง? shared libs อะไรบ้าง?
- ถ้าเลือก **Next.js** → ใช้ App Router หรือ Pages Router? ต้องการ SSR/SSG?
- ถ้าเลือก **Python** → ใช้ uv หรือ pip? Virtual env อะไร?
- ถ้าเลือก **Database** → ต้องการ migration tool ไหม? มี seed data?
- **Auth:** ต้องการระบบ authentication ไหม? (NextAuth, Clerk, Passport, custom)
- **Testing:** ใช้ test framework อะไร? (Vitest, Jest, Pytest, Go testing)
- **Linter/Formatter:** ใช้อะไร? (ESLint+Prettier, Biome, Ruff, golangci-lint)
- **CI/CD:** ใช้อะไร? (GitHub Actions, GitLab CI, ยังไม่ต้อง)
- **Deployment:** deploy ที่ไหน? (Vercel, AWS, Azure, Docker, ยังไม่ต้อง)
- **Package Manager:** ใช้อะไร? (pnpm, npm, bun, uv, go mod)

**สำคัญ:** ถามเฉพาะคำถามที่เกี่ยวข้องกับ stack ที่เลือก — อย่าถามทุกข้อถ้าไม่จำเป็น

### Phase 2: Research Best Practices

ก่อนเริ่มสร้างโปรเจค ให้ค้นหา best practices จาก internet:

1. **ค้นหาด้วย WebSearch/WebFetch:**
   - "{framework} project structure best practices {year}"
   - "{framework} + {database} setup guide"
   - ถ้าเป็น monorepo: "{monorepo-tool} setup guide {language}"
   - ถ้ามี specific library: "{library} recommended configuration"

2. **สิ่งที่ต้องค้นหา:**
   - Recommended directory structure สำหรับ stack ที่เลือก
   - Default configurations ที่ควรตั้งค่า
   - Common pitfalls / gotchas ของ stack นั้น
   - Security best practices (เช่น .env handling, CORS, CSP)
   - Performance best practices (เช่น bundling, caching)

3. **รวบรวม findings** เป็น checklist สำหรับ Phase 3

### Phase 3: Confirm Plan กับ User

ก่อนสร้างอะไร ต้องแสดง plan ให้ user เห็นก่อน:

1. **แสดง Directory Structure** ที่จะสร้าง (tree format)
2. **แสดง Dependencies** ที่จะติดตั้ง (แยก production / dev)
3. **แสดง Config Files** ที่จะสร้าง (เช่น tsconfig, eslint, prettier, .env.example)
4. **แสดง Best Practices** ที่พบจาก research พร้อมเหตุผล
5. **แสดง Trade-offs** ของแนวทางที่เลือก (ข้อดี/ข้อเสีย)

ถาม user: "ต้องการปรับอะไรไหม?" → ถ้ามีก็ปรับ plan ก่อนเริ่ม

### Phase 4: Execute — สร้างโปรเจค

ดำเนินการตาม plan ที่ confirm แล้ว:

**4.1 — Initialize Project**
- สร้าง project ด้วย official CLI/scaffolding tool ของ framework (ถ้ามี)
  - เช่น `npx create-next-app@latest`, `npx create-nx-workspace`, `uv init`
- หรือสร้าง directory structure ด้วยมือถ้าไม่มี CLI

**4.2 — Install Dependencies**
- ติดตั้ง production dependencies
- ติดตั้ง dev dependencies (linter, formatter, testing)
- ตรวจสอบว่า lock file สร้างถูกต้อง

**4.3 — Configure Tooling**
- สร้าง/อัพเดท config files:
  - Linter config (เช่น eslint.config.js, ruff.toml)
  - Formatter config (เช่น .prettierrc, biome.json)
  - TypeScript config (ถ้าใช้)
  - Test config (เช่น vitest.config.ts, pytest.ini)
  - Git config (.gitignore, .gitattributes)
- สร้าง `.env.example` พร้อม placeholder values

**4.4 — Create Base Structure**
- สร้าง directory structure ตาม plan
- สร้าง placeholder files ที่จำเป็น (เช่น index.ts, __init__.py)
- สร้าง example/boilerplate code ถ้าเหมาะสม

**4.5 — Setup Git Flow (ถ้ายังไม่มี)**
- `git flow init -d` (ถ้าติดตั้ง git-flow แล้ว)
- หรือสร้าง `develop` branch ด้วยมือ

### Phase 5: Update CLAUDE.md

อัพเดท `CLAUDE.md` ให้ตรงกับโปรเจคที่สร้าง — **นี่คือขั้นตอนสำคัญที่สุด:**

1. **Section 1 (Project Overview):** เติมชื่อและคำอธิบายโปรเจค
2. **Section 3 (Tech Stack):** เติม technology ที่ติดตั้งจริง พร้อมเวอร์ชัน
3. **Section 4 (Project Structure):** วาด tree structure จริงที่สร้าง
4. **Section 5 (Architecture):** เติม data flow ตาม stack ที่เลือก
5. **Section 6 (Dev Commands):** เติมคำสั่งจริง (dev, test, lint, build)
6. **Section 8 (Git):** เติม branch strategy ที่ตั้งค่า
7. **Section 9 (Config):** เติม environment variables และ config pattern
8. **Section 10 (Dependencies):** เติม package manager commands
9. **Section 11 (Coding Conventions):** เติม naming conventions ตามภาษา/framework
10. **Section 15 (Gotchas):** เติม known gotchas จาก research

**เฉพาะ section ที่มีข้อมูลจริง — ลบ placeholder/TODO ที่เติมแล้วออก**

### Phase 6: Validate

1. ตรวจสอบว่า project รันได้:
   - `{package-manager} install` / `{package-manager} sync` สำเร็จ
   - Dev server start ได้ (ถ้ามี)
   - Linter รันผ่าน
   - Test runner ทำงานได้ (แม้ยังไม่มี tests)
2. ตรวจสอบ `.gitignore` ครอบคลุม (node_modules, .env, build output, etc.)
3. ตรวจสอบ CLAUDE.md ไม่มี unfilled placeholders

## Output

รายงานสรุป:
- โครงสร้างที่สร้าง (tree)
- Dependencies ที่ติดตั้ง
- Config files ที่สร้าง
- คำสั่งที่ใช้เริ่มต้นทำงาน (dev, test, lint)
- สิ่งที่ user ต้องทำเอง (เช่น กรอก API keys ใน .env)

## Safety Rules

- ห้ามเขียน credentials/secrets จริงลงไฟล์ — ใช้ placeholder เสมอ
- ห้ามลบไฟล์ที่มีอยู่แล้วโดยไม่ถาม user ก่อน
- ถ้าโปรเจคมีไฟล์อยู่แล้ว → ถาม user ว่าจะ overwrite หรือ merge
- ใช้ official/stable versions ของ dependencies — ไม่ใช้ beta/canary ถ้าไม่ได้ระบุ

## Reminders

- อ่าน CLAUDE.md ก่อนเริ่มเสมอ เพื่อไม่สร้างซ้ำกับสิ่งที่มีอยู่
- ใช้ WebSearch ค้นหา best practices ก่อนตัดสินใจโครงสร้าง
- ทุก decision ต้องมีเหตุผลรองรับ — อย่าเลือกเพราะ "นิยม" อย่างเดียว
- ถาม follow-up questions ที่ smart — ไม่ถามสิ่งที่ infer ได้จากคำตอบก่อนหน้า
