# /smart-push — ประเมิน, Commit & Push Code อัจฉริยะ

ประเมิน code changes ว่าควรแยก commit หรือรวมได้ จากนั้น commit และ push ขึ้น Git

## Commit Message Format

```
[<feature name>] <commit message> (Reviewed by <Reviewer name>)
```

ตัวอย่าง:
- `[auth] add GitHub OAuth login flow (Reviewed by John)`
- `[repo-list] fix pagination bug on large repos (Reviewed by Jane)`
- `[api] add batch status endpoint (Reviewed by Somchai)`

## Process

### Step 1: รวบรวมข้อมูล

1. รัน `git status` และ `git diff --stat` เพื่อดูไฟล์ที่เปลี่ยนแปลง
2. รัน `git diff` (หรือ `git diff --cached` ถ้ามี staged files) เพื่อดูรายละเอียด code ที่เปลี่ยน
3. รัน `git log --oneline -5` เพื่อดู commit ล่าสุด
4. รัน `git branch --show-current` เพื่อดู branch ปัจจุบัน

### Step 2: ประเมิน Code Changes

วิเคราะห์ changes ทั้งหมดแล้วตัดสินใจ:

**เกณฑ์การแยก commit:**
- ถ้า changes ทั้งหมดเกี่ยวข้องกับ feature/scope เดียวกัน → **รวม commit เดียวได้**
- ถ้า changes เกี่ยวข้องกับหลาย feature/scope ที่ต่างกันชัดเจน → **ควรแยก commit**
- ถ้ามี changes ที่เป็นคนละประเภท (เช่น feat + fix + refactor) → **ควรแยก commit**
- ถ้ามีไฟล์ที่ไม่เกี่ยวข้องกัน (เช่น frontend + backend ที่ไม่เกี่ยวกัน) → **ควรแยก commit**

**ถ้าประเมินแล้วว่าต้องแยก commit:**
ใช้ AskUserQuestion แสดงแผนการแยก commit ให้ user confirm ก่อน โดยแสดง:
- จำนวน commits ที่จะแยก
- แต่ละ commit มีไฟล์อะไรบ้าง
- commit message ที่จะใช้สำหรับแต่ละ commit

### Step 3: ถาม User เรื่อง Reviewer และ Feature Name

ใช้ AskUserQuestion ถามข้อมูลที่จำเป็น:
- **Feature name** (ถ้ายังไม่ชัดเจนจาก context) — เช่น `auth`, `repo-list`, `api`
- **Reviewer name** — ชื่อคนที่ review code

### Step 4: Confirm กับ User

ใช้ AskUserQuestion ถาม user โดยแสดง:
- สรุปไฟล์ที่จะ commit (แยกตาม commit ถ้ามีหลาย commit)
- Commit message แต่ละตัวตาม format: `[<feature name>] <commit message> (Reviewed by <Reviewer name>)`
- Branch ที่จะ push

### Step 5: ดำเนินการ

เมื่อ user confirm แล้ว:

**กรณี commit เดียว:**
1. `git add` เฉพาะไฟล์ที่เกี่ยวข้อง (**ไม่ใช้** `git add -A` หรือ `git add .`)
2. `git commit -m "[<feature>] <message> (Reviewed by <name>)"`
3. `git push` ขึ้น branch ปัจจุบัน
4. แสดงผลลัพธ์ให้ user

**กรณีแยกหลาย commits:**
ทำซ้ำสำหรับแต่ละ commit ตามลำดับที่ตกลงกัน:
1. `git add` เฉพาะไฟล์ของ commit นั้น
2. `git commit -m "[<feature>] <message> (Reviewed by <name>)"`
3. ทำจนครบทุก commit
4. `git push` ขึ้น branch ปัจจุบัน (push ครั้งเดียวตอนท้าย)
5. แสดงผลลัพธ์ทั้งหมดให้ user

## Safety Rules

- ห้าม commit ไฟล์ที่มี secrets (`.env`, credentials, API keys)
- ห้าม force push (`--force`, `--force-with-lease`)
- ห้าม push ขึ้น `main` / `master` โดยไม่ได้รับอนุญาตชัดเจน
- ถ้า pre-commit hook fail → แก้ไขปัญหาแล้วสร้าง commit ใหม่ (ห้าม `--no-verify`)
- ถ้ามี uncommitted changes ที่ไม่เกี่ยวข้อง → ถาม user ว่าจะรวมหรือไม่
