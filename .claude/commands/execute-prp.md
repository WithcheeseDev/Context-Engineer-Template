# /execute-prp — Execute a PRP

ดำเนินการตาม PRP (Product Requirement Plan) ที่ระบุ

## Input

ผู้ใช้จะระบุ path ไปยัง PRP file เช่น: `/execute-prp PRPs/active/{feature-name}.md`

## Process

### Phase 1: Load PRP

1. อ่าน PRP file ที่ระบุ
2. ทำความเข้าใจ requirements, context, และ validation criteria ทั้งหมด
3. อ่าน reference files ทุกไฟล์ที่ PRP ระบุไว้ใน "Context Requirements"
4. อ่าน CLAUDE.md เพื่อทบทวน conventions

### Phase 2: Plan

1. คิดอย่างละเอียดก่อนเริ่ม implement
2. แยก tasks ออกเป็นขั้นตอนย่อย
3. ระบุ code ที่มีอยู่แล้วที่สามารถ reuse ได้
4. ตรวจสอบว่า patterns ตรงกับ codebase conventions
5. ถ้าไม่แน่ใจ — **ถาม user ก่อนเริ่ม implement**

### Phase 3: Execute

ดำเนินการตาม task list ใน PRP:
1. สร้าง/แก้ไขไฟล์ตามที่ระบุ
2. ทำตาม patterns จาก examples/
3. เขียน documentation ตาม convention ของโปรเจค
4. เพิ่ม type annotations ทุก function

### Phase 4: Validate

รัน validation gates ตามลำดับ:

**Gate 1: Linting & Formatting**
รัน lint command ตาม CLAUDE.md → ถ้า fail → แก้ไขแล้ว lint ใหม่

**Gate 2: Tests**
รัน test command ตาม CLAUDE.md → ถ้า fail → แก้ไข tests หรือ implementation แล้ว test ใหม่

**Gate 3: Integration (ถ้ามี)**
ทำตาม integration test steps ที่ PRP ระบุ

### Phase 5: Complete

1. ตรวจสอบ completion checklist ของ PRP ทุกข้อ
2. รัน final validation อีกครั้ง
3. รายงานสถานะ:
   - tasks ที่เสร็จแล้ว
   - validation results
   - สิ่งที่ยังต้องทำ (ถ้ามี)

## Iteration Rules

- ถ้า validation fail ให้ iterate จนกว่าจะผ่าน (สูงสุด 3 รอบ)
- ถ้ายังไม่ผ่านหลัง 3 รอบ ให้รายงานปัญหาและแนะนำวิธีแก้ไข
- NEVER skip validation gates
- NEVER ignore test failures

## Conventions Checklist

ก่อนรายงาน "Complete" ตรวจสอบ:
- [ ] Code ตาม conventions ใน CLAUDE.md
- [ ] ผ่าน Quality Gates ทุกข้อ (ดู CLAUDE.md section 7)
- [ ] ไม่มี hardcoded credentials หรือ secrets
- [ ] Integration points ครบทุกข้อ
- [ ] ไม่มี regression ใน functionality ที่มีอยู่
