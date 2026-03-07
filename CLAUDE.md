# CLAUDE.md — {ชื่อโปรเจค}

<!-- คำแนะนำ: แทนที่ {ชื่อโปรเจค} และ placeholder ทั้งหมดด้วยข้อมูลจริงของโปรเจค -->
<!-- ลบ comment แนะนำออกหลังกรอกเสร็จ -->

## 1. Project Overview

<!-- TODO: อธิบายว่าระบบคืออะไร ทำอะไร สำหรับใคร — 1-3 บรรทัด -->

**{ชื่อโปรเจค}** คือ {คำอธิบายสั้น ๆ ว่าระบบทำอะไร เช่น "ระบบจัดการ..." / "แพลตฟอร์ม..." / "API สำหรับ..."}

ตัวอย่าง:
> **Acme API** คือ REST API สำหรับจัดการคำสั่งซื้อ รองรับ multi-tenant พร้อม real-time notification ผ่าน WebSocket

---

## 2. กฎการทำงานของ AI Agent

กฎที่ AI Agent ต้องทำตามเสมอเมื่อทำงานกับโปรเจคนี้:

- **อ่านก่อนแก้เสมอ:** อ่านไฟล์ที่จะแก้ไขทั้งหมดก่อนเริ่มแก้ — เข้าใจ context ก่อน
- **ตรวจ examples/ ก่อนสร้าง pattern ใหม่:** ดู `examples/` ว่ามี reference ที่ตรงกับงานหรือไม่ (ดู [Examples Reference](#13-examples-reference))
- **Lint ทุกครั้งหลังแก้ไข:** รัน `{lint command}` ก่อนรายงานว่าเสร็จ
- **ถามก่อนเสมอถ้าไม่ชัดเจน:** ถ้า requirement ไม่ชัด, มีทางเลือก architecture มากกว่า 1, หรือต้องลบ/เปลี่ยน API ที่มีอยู่ → **ต้องถาม user ก่อนทุกครั้ง** | requirement ชัดเจนแล้ว → ทำเลย
- **บอกข้อดีข้อเสียเสมอ:** ทุกครั้งที่วางแผน (plan mode) ต้องระบุข้อดีและข้อเสียของแนวทางที่เลือกให้ชัดเจน
- **ห้ามเดา:** ถ้าไม่แน่ใจว่า function/API ทำงานอย่างไร ให้อ่าน source code จริง ไม่ใช่คาดเดา

<!-- TODO: เพิ่มกฎเฉพาะโปรเจค เช่น -->
<!-- - ใช้ slash commands: `/new-endpoint`, `/new-workflow`, `/quality-check` -->
<!-- - พูดคุยเป็นภาษาไทยเสมอ -->

---

## 3. Tech Stack

<!-- TODO: เติม technology ที่ใช้จริงในโปรเจค -->

| Category | Technology |
|----------|-----------|
| Language | {เช่น Python 3.12+ / TypeScript 5.x / Go 1.22+} |
| Web Framework | {เช่น FastAPI / Next.js / Express / Gin} |
| Database | {เช่น PostgreSQL 16 / MongoDB 7 / Redis} |
| ORM / Query | {เช่น SQLAlchemy 2.0 / Prisma / Drizzle} |
| AI/Agent | {เช่น LangGraph / LangChain / Semantic Kernel — ลบถ้าไม่เกี่ยว} |
| Auth | {เช่น NextAuth / Passport / Azure AD / Clerk} |
| Config | {เช่น Pydantic Settings / dotenv / Viper} |
| Package Manager | {เช่น uv / pnpm / npm / go mod} |
| Monorepo | {เช่น Nx / Turborepo / pnpm workspaces — ลบถ้าไม่ใช่ monorepo} |
| Linter/Formatter | {เช่น Ruff / ESLint + Prettier / golangci-lint} |
| Testing | {เช่น Pytest / Vitest / Jest / Go testing} |
| IaC/Deploy | {เช่น Docker / Terraform / Bicep / Vercel} |

เวอร์ชันจริงดูที่ `package.json` / `pyproject.toml` / `go.mod`

---

## 4. Project Structure

**โครงสร้างโปรเจคต้องยึดตาม `PROJECT_STRUCTURE.md` เป็นหลัก**

### กฎสำคัญ

- **อ่าน `PROJECT_STRUCTURE.md` ก่อนสร้างไฟล์/โฟลเดอร์ใหม่เสมอ** — สร้างตาม structure ที่กำหนดไว้เท่านั้น
- **ห้ามสร้างไฟล์หรือโฟลเดอร์นอก structure ที่กำหนด** — ถ้าต้องการเพิ่ม directory ใหม่ที่ไม่มีใน `PROJECT_STRUCTURE.md` ต้องถาม user ก่อนและอัพเดท `PROJECT_STRUCTURE.md` ให้ตรงกัน
- **ไฟล์ใหม่ต้องอยู่ใน directory ที่ถูกต้องตามหน้าที่** — เช่น route อยู่ใน routes/, service อยู่ใน services/

### การจัดวาง PROJECT_STRUCTURE.md

| โครงสร้างโปรเจค | ตำแหน่ง PROJECT_STRUCTURE.md | หมายเหตุ |
|----------------|------------------------------|----------|
| **Single app** | `PROJECT_STRUCTURE.md` ที่ root | ไฟล์เดียวครอบคลุมทั้งโปรเจค |
| **Monorepo** | `apps/{app-name}/PROJECT_STRUCTURE.md` ต่อแต่ละ app | แต่ละ app มี structure เป็นของตัวเอง — ไม่ใช้ไฟล์ร่วมกัน เพื่อกันสับสน |

**สำหรับ Monorepo:**
- เมื่อทำงานกับ app ใด ให้ยึด `PROJECT_STRUCTURE.md` ของ app นั้นเท่านั้น
- Root level อาจมี `PROJECT_STRUCTURE.md` สำหรับ shared structure (เช่น `libs/`, `infra/`) แยกต่างหาก
- ห้ามอ้างอิง structure ข้าม app — แต่ละ app เป็นอิสระต่อกัน

### ภาพรวมโครงสร้าง

<!-- TODO: วาด tree structure ของโปรเจค — ปรับตามโครงสร้างจริง -->
<!-- ต้องตรงกับ PROJECT_STRUCTURE.md — ถ้าแก้ที่นี่ต้องแก้ที่ PROJECT_STRUCTURE.md ด้วย -->

```
{project-name}/
├── apps/                        # Applications
│   └── {app-name}/              # แอปหลัก
│       └── src/
│           ├── routes/          # API routes / pages
│           ├── services/        # Business logic
│           ├── middleware/       # Middleware
│           └── utils/           # Utilities
├── libs/                        # Shared libraries
│   ├── {lib-1}/                 # {คำอธิบาย เช่น core config + exceptions}
│   ├── {lib-2}/                 # {คำอธิบาย เช่น shared models}
│   └── {lib-3}/                 # {คำอธิบาย เช่น database client}
├── examples/                    # Reference implementations สำหรับ AI
├── infra/                       # Infrastructure as Code
├── PROJECT_STRUCTURE.md         # Source of truth สำหรับโครงสร้างโปรเจค
├── INITIAL.md                   # Initial project setup guide
├── {config-file}                # เช่น pyproject.toml / package.json
└── CLAUDE.md                    # ไฟล์นี้
```

<!-- สำหรับ monorepo: เพิ่ม sub-CLAUDE.md ในแต่ละ app/lib ที่มี context เฉพาะ -->
<!-- เอกสาร sub-project: `apps/{name}/CLAUDE.md` · `libs/{name}/CLAUDE.md` -->

---

## 5. Architecture & Workflow

### Data Flow

<!-- TODO: วาด data flow หลักของระบบ — ปรับตาม architecture จริง -->

```
[Client] → [API Gateway / Load Balancer]
                    ↓
            [App Server / Framework]
                    ↓
            [Business Logic / Service Layer]
                    ↓
        ┌───────────┴───────────┐
        ↓                       ↓
  [Database]              [External Services]
        ↓                       ↓
  [Cache Layer]           [Message Queue]
        ↓                       ↓
    [Response]            [Async Workers]
```

<!-- TODO: อธิบาย key flows เพิ่มเติม เช่น -->
<!-- ### Authentication Flow -->
<!-- ### Background Job Pipeline -->
<!-- ### Event-Driven Flow -->

### Key Architectural Decisions

<!-- TODO: ระบุ decisions สำคัญ เช่น -->

- **{Decision 1}:** {เช่น "ส่ง dependencies ผ่าน DI container ไม่ใช่ global state"}
- **{Decision 2}:** {เช่น "ใช้ event-driven architecture ระหว่าง services ผ่าน message queue"}
- **{Decision 3}:** {เช่น "แยก read/write models (CQRS) สำหรับ high-traffic endpoints"}

---

## 6. Development Commands

<!-- TODO: เปลี่ยนคำสั่งให้ตรงกับโปรเจคจริง -->

```bash
# Setup
{package-manager} install          # ติดตั้ง dependencies
cp .env.example .env               # สร้างไฟล์ config

# Run
{package-manager} run dev          # เริ่ม dev server (hot-reload)
{package-manager} run dev:{app}    # เริ่ม dev server เฉพาะ app

# Quality
{package-manager} run test         # รัน tests ทั้งหมด
{package-manager} run lint         # รัน linter
{package-manager} run typecheck    # ตรวจ types (ถ้ามี)
{package-manager} run format       # Format code

# Build & Deploy
{package-manager} run build        # Production build
{package-manager} run build:{app}  # Build เฉพาะ app
```

<!-- เพิ่มคำสั่ง infra ถ้ามี เช่น docker-compose, terraform -->

---

## 7. Quality Gates (Definition of Done)

ก่อนรายงานว่างานเสร็จ ต้องผ่านทุกข้อ:

- [ ] Linter ผ่านไม่มี error
- [ ] Tests ผ่านทั้งหมด (ทั้ง unit tests ที่มีอยู่เดิมและที่เขียนใหม่)
- [ ] ไม่มี hardcoded credentials/secrets ใน code
- [ ] ไม่มี debug statements หลงเหลือ (เช่น `print()`, `console.log()` ที่ไม่จำเป็น)
- [ ] มี type annotations / type hints ทุก function signature ใหม่
- [ ] Code ใหม่มี documentation ตาม convention ของโปรเจค

<!-- TODO: เพิ่ม quality gates เฉพาะโปรเจค เช่น -->
<!-- - [ ] Docstrings ภาษาไทยบน public functions ใหม่ทุกตัว -->
<!-- - [ ] Exceptions สืบทอดจาก {BaseError} -->
<!-- - [ ] Migration file สร้างแล้ว (ถ้าแก้ schema) -->

---

## 8. Git & Branch Conventions

### Branch Strategy

<!-- TODO: ปรับตาม branching model ของทีม -->

| Branch | หน้าที่ |
|--------|---------|
| `main` / `master` | Production — deploy อัตโนมัติ |
| `develop` | Development — รวม feature ก่อน release |
| `feature/{name}` | Feature ใหม่ |
| `fix/{name}` | Bug fix |
| `refactor/{name}` | Refactoring |
| `chore/{name}` | งาน maintenance |

### Commit Format

<!-- TODO: ใส่ format จริงของทีม -->

```
{prefix} {commit message}
```

ตัวอย่าง:
- Conventional Commits: `feat(auth): add OAuth2 login flow`
- Custom format: `[-][-] add OAuth2 login flow (Reviewed by {Name})`

### PR Rules

- **PR target:** `develop` เสมอ (ไม่ merge ตรงไป `main`)
- **AI commits:** เพิ่ม `Co-Authored-By: Claude <noreply@anthropic.com>` ใน footer

---

## 9. Configuration

<!-- TODO: อธิบาย config pattern ของโปรเจค -->

### Environment Variables

ทุก environment variable ใช้ prefix `{PREFIX}_` — ดูตัวอย่างที่ `.env.example`

```env
{PREFIX}_APP_NAME={project-name}
{PREFIX}_DEBUG=false
{PREFIX}_LOG_LEVEL=INFO
{PREFIX}_DATABASE_URL=postgresql://localhost:5432/{db-name}
{PREFIX}_REDIS_URL=redis://localhost:6379/0
{PREFIX}_SECRET_KEY=...
```

### Settings Loader

<!-- TODO: อธิบายวิธีโหลด config เช่น -->
<!-- Settings โหลดผ่าน Pydantic Settings (`libs/core/config.py`) — ใช้ `extra="ignore"` -->
<!-- หรือ Config โหลดผ่าน dotenv + zod validation (`src/config/env.ts`) -->

Settings โหลดผ่าน `{path-to-config}` — ใช้ {library/pattern} สำหรับ validation

---

## 10. Dependency Management

<!-- TODO: ปรับให้ตรงกับ package manager ของโปรเจค -->

| Action | Command |
|--------|---------|
| เพิ่ม package | `{เช่น uv add <pkg> --package <workspace>}` |
| เพิ่ม dev dependency | `{เช่น uv add --dev <pkg>}` |
| Sync/Install | `{เช่น uv sync}` |
| อัพเดท package | `{เช่น uv update <pkg>}` |

### กฎสำคัญ

- Sync ทุกครั้งหลังเปลี่ยน dependencies
- Lock file (`{เช่น uv.lock / pnpm-lock.yaml}`) ต้อง commit เสมอ

<!-- สำหรับ monorepo: -->
<!-- - Workspace reference: เพิ่มชื่อ package ใน dependencies + workspace source config -->
<!-- - Dev dependencies แชร์ผ่าน root config -->

---

## 11. Coding Conventions

### Naming Conventions

<!-- TODO: เพิ่ม/ปรับ naming conventions ตามภาษาและ framework -->

| หมวด | Convention | ตัวอย่าง |
|------|-----------|---------|
| Files (components) | {เช่น PascalCase} | `UserProfile.tsx` |
| Files (modules) | {เช่น snake_case} | `user_service.py` |
| Functions/Methods | {เช่น camelCase / snake_case} | `getUserById` / `get_user_by_id` |
| Classes | PascalCase | `OrderService` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT` |
| Interfaces/Types | {เช่น PascalCase + suffix} | `UserProfileProps` / `OrderResponse` |

### Style Rules

- Line length: **{เช่น 120 / 100 / 80}** characters
- ชื่อตัวแปร: ใช้ชื่อที่สื่อความหมาย — ห้ามใช้ชื่อสั้น ๆ แบบ `i`, `j` (ใช้ `idx`, `retryCount`)
- Import order: {อธิบาย import order ของโปรเจค}

<!-- ตัวอย่าง: -->
<!-- Import: stdlib → third-party → workspace libs → relative → type imports -->

### Error Handling

<!-- TODO: ปรับตาม error handling pattern ของโปรเจค -->

- Custom errors สืบทอดจาก `{BaseError}` ที่ `{path}`
- ใช้ `logging.getLogger(__name__)` / `console.error('[Context]', err)` — ไม่ใช่ `print()` / `console.log()`
- Handle unknown errors: `err instanceof Error ? err.message : 'Unknown error'`

### Method Ordering (ภายใน class)

<!-- TODO: ระบุลำดับ methods — ตัวอย่าง: -->

1. Constructor / `__init__`
2. Lifecycle methods (เช่น `__aenter__`, `componentDidMount`)
3. Abstract / interface methods
4. **Public methods — ต้องอยู่ก่อน private เสมอ** เพื่อให้อ่าน API ของ class ได้ทันทีโดยไม่ต้อง scroll ผ่าน implementation details
5. Private methods (`_` prefix / `#` private)

### Documentation & File Context

<!-- TODO: ระบุ convention สำหรับ docstrings / comments -->

- Docstrings/Comments เขียนเป็น {ภาษาไทย / ภาษาอังกฤษ}
- Public functions ใหม่ทุกตัวต้องมี docstring
- ใช้ {format เช่น Google style / JSDoc / GoDoc}

#### Context Engineering — เขียน Context ไว้ในไฟล์

ทุกไฟล์ที่สร้างใหม่ต้องมี **file header comment** อธิบาย context สั้น ๆ ที่หัวไฟล์ เพื่อให้ AI agent เข้าใจได้ทันทีโดยไม่ต้องอ่านทั้งไฟล์:

```
// ไฟล์นี้ทำอะไร: {คำอธิบายสั้น ๆ}
// ใช้กับ: {module/feature ที่เกี่ยวข้อง}
// ข้อควรระวัง: {gotcha สำคัญ ถ้ามี}
```

**หลักการ 3 ระดับ:**

| ระดับ | วิธีให้ Context | ตัวอย่าง |
|-------|----------------|----------|
| **โปรเจค** | เขียนไว้ใน `CLAUDE.md`, `PROJECT_STRUCTURE.md` | ภาพรวม, กฎ, conventions |
| **ไฟล์** | เขียน header comment ที่หัวไฟล์ | ไฟล์นี้ทำอะไร, ใช้กับอะไร, ข้อควรระวัง |
| **Implementation** | ให้ agent อ่าน code จริง | รายละเอียด logic, ตรวจสอบว่า comment ยังตรงกับ code |

**เหตุผล:** เขียน context ไว้ = ประหยัด token + ได้ทั้ง what/why/constraints ทันที ส่วนการอ่าน code จริง = ตรวจสอบความถูกต้อง เพราะ comment อาจ outdated แต่ code คือ truth

### Testing Conventions

- Test files: `{เช่น test_*.py / *.test.ts / *_test.go}` อยู่ {colocate กับ source / แยก `tests/`}
- ใช้ {test framework} + {assertion library}
- Naming: `{เช่น test_{behavior} / describe('...', () => it('should...'))}`

---

## 12. Task Recipes

<!-- TODO: เพิ่ม recipes เฉพาะโปรเจค — "ถ้าจะทำ X ให้ทำ Y" -->

| งาน | วิธีทำ |
|-----|--------|
| สร้าง API endpoint ใหม่ | {เช่น ดู `examples/api/` หรือ ใช้ `/new-endpoint`} |
| สร้าง component ใหม่ | {เช่น ดู `examples/components/` — ทำตาม barrel export pattern} |
| สร้าง database migration | {เช่น `{tool} migrate create {name}` แล้วแก้ไข SQL} |
| เพิ่ม shared library ใหม่ | {เช่น สร้าง `libs/{name}/` + config + เพิ่มใน workspace + sync} |
| เขียน tests | {เช่น ดู `examples/tests/` — ใช้ pattern ที่กำหนด} |
| Feature ซับซ้อน | {เช่น ใช้ `/generate-prp` สร้าง PRP แล้ว `/execute-prp` ดำเนินการ} |

---

## 13. Design Patterns

<!-- TODO: อธิบาย patterns หลักที่ใช้ในโปรเจค -->

### {Pattern 1: เช่น Repository Pattern}

{คำอธิบายสั้น ๆ ว่า pattern นี้ใช้ที่ไหน ทำไม}

- **ตัวอย่าง:** `{path/to/example}`
- **ใช้เมื่อ:** {สถานการณ์ที่ควรใช้}

### {Pattern 2: เช่น Factory Pattern}

{คำอธิบาย}

- **ตัวอย่าง:** `{path/to/example}`
- **ใช้เมื่อ:** {สถานการณ์}

### {Pattern 3: เช่น Observer / Pub-Sub}

{คำอธิบาย}

- **ตัวอย่าง:** `{path/to/example}`
- **ใช้เมื่อ:** {สถานการณ์}

<!-- เพิ่ม patterns ตามที่โปรเจคใช้จริง -->

---

## 14. Examples Reference

โฟลเดอร์ `examples/` มี annotated reference implementations — **อ่านก่อนสร้าง code ใหม่เสมอ:**

<!-- TODO: เพิ่มไฟล์ตัวอย่างของโปรเจค -->

| File | Pattern | ใช้เมื่อ |
|------|---------|----------|
| `examples/{category}/{file}` | {ชื่อ pattern} | {สถานการณ์ที่ต้องดู} |
| `examples/{category}/{file}` | {ชื่อ pattern} | {สถานการณ์} |
| `examples/{category}/{file}` | {ชื่อ pattern} | {สถานการณ์} |

<!-- ตัวอย่าง: -->
<!-- | `examples/api/rest_endpoint.py` | REST endpoint + validation | สร้าง/แก้ไข API endpoint | -->
<!-- | `examples/components/DataTable.tsx` | Table + pagination | สร้าง data table component | -->
<!-- | `examples/tests/test_patterns.py` | Test structure + mocking | เขียน tests ใหม่ | -->

---

## 15. Known Gotchas & Anti-patterns

<!-- TODO: ใส่สิ่งที่ต้องระวังเฉพาะโปรเจค — เรียงจากสำคัญที่สุดไปน้อยที่สุด -->

### ต้องระวัง (Gotchas)

- **{Gotcha 1}:** {เช่น "SDK callbacks ทำงานใน background thread — ต้องใช้ thread-safe mechanism ส่งกลับ event loop"}
- **{Gotcha 2}:** {เช่น "Config singleton สร้างที่ module level — ถ้า env vars ยังไม่พร้อมจะ error ทันที"}
- **{Gotcha 3}:** {เช่น "CSS framework ใช้ config ใน CSS ไม่ใช่ JS config file — ห้ามสร้าง config file"}

### ห้ามทำ (Anti-patterns)

- **NEVER:** {เช่น "อย่าส่ง credentials/secrets ผ่าน application state — ส่งผ่าน config/DI เท่านั้น"}
- **NEVER:** {เช่น "อย่า hardcode URLs — ใช้ environment variables เสมอ"}
- **NEVER:** {เช่น "อย่าใช้ `any` type — ถ้าไม่รู้ type ให้ใช้ `unknown` แล้ว narrow"}

### หมายเหตุ (Notes)

- **Note:** {เช่น "ไฟล์ X อ้างอิง resource Y ที่ยังไม่มี — fail เงียบ ไม่ใช่ bug"}
- **Note:** {เช่น "eslint-disable ใน file Z ตั้งใจ — ไม่ใช่ bug"}
