# Examples — Reference Implementations

ไฟล์ในโฟลเดอร์นี้คือตัวอย่างจาก code จริงในโปรเจค เพื่อให้ AI coding agent เข้าใจ pattern ที่ถูกต้อง

## วิธีเพิ่มตัวอย่าง

1. **คัดลอก code จริง** จาก codebase มาเป็น reference (ไม่ใช่เขียนใหม่)
2. **เพิ่ม annotations** อธิบาย pattern สำคัญด้วย comments:
   - `# PATTERN:` — อธิบาย pattern ที่ใช้
   - `# GOTCHA:` — สิ่งที่ต้องระวัง
   - `# CRITICAL:` — สิ่งที่ห้ามพลาด
3. **อัพเดทตารางด้านล่าง** เมื่อเพิ่มไฟล์ใหม่
4. **อัพเดท CLAUDE.md** section "Examples Reference" ให้ตรงกัน

## ดัชนี Pattern

<!-- TODO: เพิ่มไฟล์ตัวอย่างของโปรเจค -->

| ไฟล์ | Pattern | ต้นฉบับ |
|------|---------|--------|
| `{category}/{file}` | {ชื่อ pattern} | `{path/to/original/source}` |

<!-- ตัวอย่าง: -->
<!-- | `api/rest_endpoint.py` | REST endpoint + validation + DI | `apps/api/src/routes/users.py` | -->
<!-- | `components/DataTable.tsx` | Table + sorting + pagination | `apps/web/src/features/users/UserTable.tsx` | -->
<!-- | `hooks/useWebSocket.ts` | Generic WebSocket hook + reconnection | `apps/web/src/hooks/useWebSocket.ts` | -->
<!-- | `tests/test_patterns.py` | Test class structure + mocking | `apps/api/tests/test_users.py` | -->

## วิธีใช้

เมื่อสร้าง code ใหม่ ให้ดูตัวอย่างที่ตรงกับ pattern ที่ต้องการ:

<!-- TODO: เพิ่ม mapping ว่า "ถ้าจะทำ X → ดู Y" -->

- สร้าง {type 1} ใหม่ → ดู `{category}/{file}`
- สร้าง {type 2} ใหม่ → ดู `{category}/{file}`
- เขียน tests → ดู `{tests/file}`

## โครงสร้างแนะนำ

```
examples/
├── README.md              # ไฟล์นี้
├── api/                   # API endpoint patterns
├── components/            # UI component patterns
├── hooks/                 # Hook / utility patterns
├── services/              # Business logic patterns
└── tests/                 # Testing patterns
```

จัดหมวดหมู่ตาม domain ของโปรเจค — ไม่จำเป็นต้องใช้โครงสร้างด้านบนทุกอย่าง
