# /quality-check — รัน Full Quality Check Pipeline

รัน linting, tests, และ convention validation ทั้งหมด

## Process

### Step 1: Lint & Format

<!-- TODO: เปลี่ยนคำสั่งให้ตรงกับโปรเจคจริง -->

```bash
{lint command จาก CLAUDE.md section 6}
```

ถ้า fail: แก้ไข lint errors ตาม convention ของโปรเจค

### Step 2: Tests

```bash
{test command จาก CLAUDE.md section 6}
```

ถ้า fail: ตรวจสอบ test failures และแก้ไข

### Step 3: Type Check (ถ้ามี)

```bash
{typecheck command — ลบถ้าไม่มี}
```

### Step 4: Convention Check

ตรวจสอบด้วยตนเอง (ดู CLAUDE.md section 7 — Quality Gates):

- [ ] ไม่มี debug statements หลงเหลือ (`print()`, `console.log()` ที่ไม่จำเป็น)
- [ ] ไม่มี hardcoded credentials/secrets
- [ ] ทุก function ใหม่มี type annotations
- [ ] Code ใหม่มี documentation ตาม convention
- [ ] ไม่มี TODO/FIXME ที่ลืมจัดการ

<!-- TODO: เพิ่ม convention checks เฉพาะโปรเจค เช่น -->
<!-- - [ ] Docstrings เป็นภาษาไทย -->
<!-- - [ ] Exceptions สืบทอดจาก {BaseError} -->
<!-- - [ ] Logging ใช้ logger pattern -->

### Step 5: Report

รายงานผลลัพธ์:
- **Lint:** PASS/FAIL (จำนวน errors ถ้ามี)
- **Tests:** PASS/FAIL (จำนวน tests — passed / failed / skipped)
- **Types:** PASS/FAIL (ถ้ามี)
- **Conventions:** รายการ issues ที่พบ (ถ้ามี)

## Quick Fix Patterns

### Line too long
```
# แยกบรรทัดที่ยาวเกินกำหนด
# ดู CLAUDE.md section 11 สำหรับ line length limit
```

### Missing type annotations
```
# เพิ่ม type hints ทุก parameter + return type
# ดู CLAUDE.md section 11 สำหรับ type hint convention
```

### Debug statements
```
# ลบ print() / console.log() ที่ไม่จำเป็น
# ใช้ logging framework ตาม convention แทน
```
