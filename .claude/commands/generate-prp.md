# /generate-prp — สร้าง PRP จาก Feature Request

สร้าง Product Requirement Plan (PRP) สำหรับ feature ใหม่ ใช้ context จาก INITIAL.md หรือคำอธิบายจากผู้ใช้

## Input

ผู้ใช้จะระบุ feature ผ่าน:
1. INITIAL.md ที่กรอกแล้ว (ดู `INITIAL.md` สำหรับ template)
2. คำอธิบาย feature โดยตรง

## Process

### Phase 1: Research & Analysis

1. อ่าน INITIAL.md (ถ้ามี) เพื่อเข้าใจ feature ที่ต้องการ
2. อ่าน CLAUDE.md เพื่อเข้าใจ conventions และ patterns ของโปรเจค
3. ค้นหา codebase สำหรับ patterns ที่เกี่ยวข้อง:
   - ดู `examples/` สำหรับ reference implementations
   - ดู source code จริงที่คล้ายกับ feature ใหม่
   - ระบุ integration points (config, routes, models, exports)
4. ค้นหา documentation ภายนอกที่จำเป็น
5. ระบุ dependencies ระหว่าง tasks

### Phase 2: Context Compilation

รวบรวม context ทั้งหมด:
- Documentation URLs พร้อม section เฉพาะ
- Code snippets จาก codebase ที่เป็น pattern ต้นแบบ
- Library quirks และ version considerations
- Architectural decisions ที่มีอยู่แล้ว

### Phase 3: Blueprint Creation

สร้าง PRP จาก template `PRPs/templates/PRP-TEMPLATE.md`:
- Pseudocode สำหรับแต่ละ task พร้อม PATTERN/GOTCHA/CRITICAL annotations
- ระบุ file paths ที่ต้อง create/modify
- Error handling protocols ตาม convention ของโปรเจค
- Sequenced task list พร้อม dependencies

### Phase 4: Validation Design

กำหนด validation gates:
1. Lint/Format check
2. Unit tests
3. Integration/Manual testing steps

## Output

บันทึก PRP ที่ `PRPs/active/{feature-name}.md`

## Quality Assessment

ให้คะแนน Confidence Score 1-10:
- ตรวจสอบว่า context ครบถ้วนหรือไม่
- มี examples ที่เกี่ยวข้องหรือไม่
- anti-patterns ครอบคลุมหรือไม่
- ถ้า score < 7 ให้แนะนำว่าต้องเพิ่ม context อะไรบ้าง

## Reminders

- ดู CLAUDE.md สำหรับ coding conventions ทั้งหมด
- ดู examples/ สำหรับ patterns ที่ถูกต้อง
- อ่าน Known Gotchas ใน CLAUDE.md ก่อนเขียน anti-patterns
- ตรวจสอบว่า PRP ไม่ขัดกับ architectural decisions ที่มีอยู่
