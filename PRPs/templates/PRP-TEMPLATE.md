# PRP: {ชื่อ Feature}

> สร้างจาก INITIAL.md เมื่อ: {วันที่}
> สถานะ: draft | in-progress | completed
> Confidence Score: {1-10} (ความมั่นใจว่า AI agent จะ implement สำเร็จใน pass เดียว)

---

## 1. Goal & Why

### สิ่งที่ต้องสร้าง
<!-- อธิบาย feature อย่างชัดเจน ไม่คลุมเครือ -->

### ทำไมถึงต้องการ
<!-- Business value หรือ technical need -->

### User Story
ในฐานะ {บทบาท} ฉันต้องการ {ความสามารถ} เพื่อ {ประโยชน์}

### Acceptance Criteria
- [ ] {criteria 1}
- [ ] {criteria 2}
- [ ] {criteria 3}

---

## 2. Context Requirements

### Codebase Patterns ที่ต้องดู

<!-- ระบุ file paths จริงที่ AI agent ต้องอ่านก่อน implement -->

```
# อ่านก่อนเริ่ม:
{path/to/reference-1}     # {คำอธิบาย pattern}
{path/to/reference-2}     # {คำอธิบาย pattern}
{path/to/reference-3}     # {คำอธิบาย pattern}
```

### Documentation ภายนอก

<!-- URLs พร้อมระบุ section เฉพาะ -->

- {URL} — ดูหัวข้อ "{section}"

### Library Quirks & Version Notes

<!-- เรื่องที่ต้องรู้เกี่ยวกับ library versions, breaking changes, known issues -->

---

## 3. Implementation Blueprint

### 3.1 Data Models

```
# PATTERN: ใช้ {model pattern ของโปรเจค เช่น Pydantic BaseModel / Zod schema / TypedDict}
{pseudocode สำหรับ data models}
```

### 3.2 Task List (เรียงตามลำดับ)

#### Task 1: {ชื่อ task}
- **File:** `{path/to/file}`
- **Action:** CREATE | MODIFY
- **Pattern:** ดู `{path/to/reference}`

```
# Pseudocode พร้อม annotations:
# PATTERN: {pattern ที่ต้องทำตาม}
# GOTCHA: {สิ่งที่ต้องระวัง}
# CRITICAL: {สิ่งที่ห้ามพลาด}
```

#### Task 2: {ชื่อ task}
<!-- เพิ่มตามจำนวน tasks -->

### 3.3 Integration Points

<!-- ระบุจุดที่ต้องเชื่อมต่อกับ code ที่มีอยู่ -->

- [ ] {เช่น Config: เพิ่ม env var ใน settings}
- [ ] {เช่น Routes: register router ใน app factory}
- [ ] {เช่น Dependencies: เพิ่ม provider ใน DI container}
- [ ] {เช่น Models: เพิ่ม types/schemas}
- [ ] {เช่น Exports: update barrel exports}

---

## 4. Validation Loop

### Gate 1: Linting & Formatting
```bash
{lint command}
# Expected: All checks passed (0 errors)
```

### Gate 2: Unit Tests
```bash
{test command}
# Expected: All tests pass
```

```
# Test template:
{pseudocode สำหรับ test structure ตาม convention ของโปรเจค}
```

### Gate 3: Integration / Manual Testing
```
# ทดสอบ end-to-end flow:
# 1. {setup step}
# 2. {test step}
# 3. {verify step}
```

---

## 5. Anti-Patterns to Avoid

- [ ] อย่า replicate code จาก reference โดยไม่ปรับให้เข้ากับ context ใหม่
- [ ] อย่าข้าม validation gates — ถ้า lint fail ต้องแก้ก่อนไปขั้นถัดไป
- [ ] {anti-pattern เฉพาะ feature นี้}
- [ ] {anti-pattern เฉพาะ feature นี้}

---

## 6. Completion Checklist

- [ ] ทุก validation gates ผ่าน
- [ ] Acceptance criteria ครบทุกข้อ
- [ ] Integration points ครบทุกข้อใน section 3.3
- [ ] ไม่มี hardcoded credentials หรือ secrets
- [ ] ไม่มี regression ใน functionality ที่มีอยู่
- [ ] Code ตาม conventions ของโปรเจค (ดู CLAUDE.md)
- [ ] {เพิ่ม criteria เฉพาะ feature}
