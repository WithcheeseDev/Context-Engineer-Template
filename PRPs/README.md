# PRPs — Product Requirement Plans

PRP คือเอกสารที่รวบรวม context ทั้งหมดที่ AI coding agent ต้องการเพื่อ implement feature ใหม่ได้สำเร็จใน pass เดียว

## Workflow

```
INITIAL.md (feature request) → /generate-prp → PRPs/active/{feature}.md → /execute-prp → Implementation
```

1. **เขียน INITIAL.md** — กรอก 4 sections (FEATURE, EXAMPLES, DOCUMENTATION, OTHER CONSIDERATIONS)
2. **สร้าง PRP** — ใช้ `/generate-prp` พร้อมระบุ INITIAL.md หรืออธิบาย feature โดยตรง
3. **Execute PRP** — ใช้ `/execute-prp PRPs/active/{feature}.md`
4. **จัดการ PRP** — เมื่อเสร็จแล้ว ย้ายจาก `active/` หรือลบ

## Directory Structure

```
PRPs/
├── templates/
│   └── PRP-TEMPLATE.md    # Template สำหรับสร้าง PRP ใหม่
├── active/                 # PRP ที่กำลังดำเนินการ
└── README.md               # ไฟล์นี้
```

## PRP Structure (6 Sections)

| Section | เนื้อหา |
|---------|---------|
| 1. Goal & Why | อะไร ทำไม acceptance criteria |
| 2. Context Requirements | Codebase patterns, docs URLs, library quirks |
| 3. Blueprint | Data models, task list, integration points |
| 4. Validation Loop | Lint, tests, integration steps |
| 5. Anti-Patterns | สิ่งที่ห้ามทำเฉพาะ feature นี้ |
| 6. Completion Checklist | เกณฑ์ความสำเร็จ |

## Confidence Score

ทุก PRP มี confidence score 1-10 (ความมั่นใจว่า AI agent จะ implement สำเร็จ):

| Score | ความหมาย | แนะนำ |
|-------|----------|-------|
| 8-10 | AI agent น่าจะ implement สำเร็จใน pass เดียว | Execute ได้เลย |
| 5-7 | อาจต้อง 2-3 iterations | เพิ่ม context ถ้าทำได้ |
| 1-4 | ต้องเพิ่ม context เพิ่มเติมก่อน execute | ห้าม execute — เพิ่ม examples, docs, anti-patterns ก่อน |
