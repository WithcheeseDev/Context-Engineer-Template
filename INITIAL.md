# INITIAL.md — Feature Request Template

> ใช้ template นี้เพื่ออธิบาย feature ใหม่ให้ AI coding agent เข้าใจได้ครบถ้วน
> เมื่อกรอกแล้ว ใช้ `/generate-prp` เพื่อสร้าง PRP จาก INITIAL นี้

---

## FEATURE (ฟีเจอร์)

<!-- อธิบาย feature ที่ต้องการสร้างอย่างละเอียด ระบุ: -->
<!-- - ต้องการอะไร (What) -->
<!-- - ทำไมถึงต้องการ (Why) -->
<!-- - Acceptance criteria ที่ชัดเจน -->
<!-- - API contract / UI behavior ถ้ามี -->

**ชื่อ**: {ชื่อ Feature}

**คำอธิบาย**: {อธิบายสั้น ๆ ชัดเจนว่า feature นี้ทำอะไร}

**User Story**: ในฐานะ {บทบาท} ฉันต้องการ {ความสามารถ} เพื่อ {ประโยชน์}

**ขอบเขต**:
- [ ] {ระบุ app/module ที่ได้รับผลกระทบ เช่น apps/web/, libs/core/}
- [ ] {เพิ่มตามจำนวน areas ที่เกี่ยวข้อง}

**Acceptance Criteria**:
- [ ] {criteria 1}
- [ ] {criteria 2}
- [ ] {criteria 3}

ตัวอย่าง:
```
ชื่อ: User Profile Page
คำอธิบาย: หน้าแสดงข้อมูล profile ของ user พร้อม edit form
User Story: ในฐานะ user ฉันต้องการดูและแก้ไขข้อมูล profile ของตัวเอง เพื่อจัดการบัญชีได้สะดวก

Acceptance Criteria:
- แสดงข้อมูล: ชื่อ, email, avatar, role
- กดปุ่ม Edit เพื่อเปิด form แก้ไข
- Validate input ก่อน submit (email format, ชื่อไม่ว่าง)
- แสดง success/error notification หลัง save
```

---

## EXAMPLES (ตัวอย่าง)

<!-- ชี้ไปที่ reference implementations จาก examples/ หรือ source code จริง -->
<!-- อธิบายว่าแต่ละตัวอย่างเกี่ยวข้องกับ feature ใหม่อย่างไร -->

1. **Pattern ที่ตรงกับ feature**:
   - ดู `examples/{category}/{file}` — {อธิบายว่าเกี่ยวข้องอย่างไร}
   - ดู `{path/to/existing-code}` — reference จริงที่คล้ายกัน

2. **Pattern เพิ่มเติม**:
   - ดู `examples/{category}/{file}` — {คำอธิบาย}

ตัวอย่าง:
```
1. Page layout pattern:
   - ดู examples/components/ProfilePage.tsx — page layout ที่คล้ายกัน
   - ดู apps/web/src/features/dashboard/DashboardPage.tsx — reference จริง

2. Form pattern:
   - ดู examples/components/EditForm.tsx — form + validation
   - ดู apps/web/src/features/settings/SettingsForm.tsx — form จริงที่มีอยู่
```

---

## DOCUMENTATION (เอกสาร)

<!-- ระบุ documentation URLs ที่เกี่ยวข้อง — ชี้ไปที่ section เฉพาะ ไม่ใช่แค่ homepage -->
<!-- รวมถึง library docs, API docs, design specs -->

### ไฟล์ที่เกี่ยวข้องในโปรเจค
- {รายการไฟล์ที่มีอยู่แล้วที่เกี่ยวข้องกับ feature นี้}

### External Documentation
- {Library/API docs URL} — ดูหัวข้อ "{section เฉพาะ}"

### Design Patterns
- {ควรใช้ pattern ที่มีอยู่ตัวไหน? อ้างอิง file path}

ตัวอย่าง:
```
ไฟล์ที่เกี่ยวข้อง:
- apps/web/src/features/auth/LoginPage.tsx — form pattern ที่ใช้อยู่
- libs/shared/ui/src/lib/forms/ — shared form components

External Documentation:
- React Hook Form: https://react-hook-form.com/get-started#SchemaValidation
  - ดูหัวข้อ "Schema Validation" สำหรับ zod integration
- Zod: https://zod.dev/?id=strings
  - ดูหัวข้อ "Strings" สำหรับ email validation

Design Patterns:
- ใช้ form pattern เดียวกับ SettingsForm (react-hook-form + zod)
```

---

## OTHER CONSIDERATIONS (ข้อพิจารณาอื่น ๆ)

<!-- นี่คือส่วนที่สำคัญที่สุด — ระบุ edge cases, gotchas, และข้อควรระวัง -->
<!-- AI coding agents มักพลาดตรงนี้ ยิ่งละเอียดยิ่งดี -->

### Edge Cases
- {เกิดอะไรขึ้นเมื่อ...?}
- {พฤติกรรมเมื่อไม่มีข้อมูล / loading / error?}
- {พฤติกรรมบน mobile / tablet?}

### Performance
- {มีข้อกังวลด้านประสิทธิภาพไหม?}
- {ข้อมูลจำนวนมาก, real-time updates, lazy loading?}

### Security
- {ต้องการ authentication / authorization ไหม?}
- {ความอ่อนไหวของข้อมูล?}
- {Input validation / sanitization?}

### Accessibility
- {การนำทางด้วย keyboard?}
- {รองรับ screen reader?}

### ข้อจำกัดที่ทราบ
- {มีข้อจำกัดจาก CLAUDE.md ที่เกี่ยวข้องไหม?}
- {มี Known Gotchas ที่ต้องระวังไหม?}

ตัวอย่าง:
```
Edge Cases:
- ถ้า user ยังไม่มี avatar → แสดง placeholder icon
- ถ้า API error ขณะ save → แสดง error toast + ไม่ clear form data
- ถ้า session หมดอายุขณะ edit → redirect ไป login

Performance:
- Avatar upload ต้อง compress ก่อน upload (max 1MB)
- ใช้ optimistic update สำหรับ profile name

Security:
- ต้อง validate email format ทั้ง client + server side
- ห้ามแสดง password ใน profile page
```
