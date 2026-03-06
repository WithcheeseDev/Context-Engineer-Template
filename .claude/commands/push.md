# /push — Stage, Commit & Push Code

Stage, commit และ push โค้ดขึ้น Git ด้วยรูปแบบ commit message มาตรฐานของทีม

## Process

### Step 1: รวบรวมข้อมูล

1. รัน `git status` และ `git diff --stat` เพื่อดูไฟล์ที่เปลี่ยนแปลง
2. รัน `git log --oneline -5` เพื่อดูรูปแบบ commit ล่าสุด
3. รัน `git branch --show-current` เพื่อดู branch ปัจจุบัน

### Step 2: ระบุข้อมูล Commit

<!-- TODO: ปรับตาม commit convention ของทีม (ดู CLAUDE.md section 8) -->

ถ้าโปรเจคใช้ task/issue tracking:
- ค้นหา Task ID จากบริบทการสนทนา (PRP, Jira, GitHub Issue)
- ถ้าหาไม่เจอ → ถาม user ด้วย AskUserQuestion

ถ้าโปรเจคมี reviewer convention:
- ถาม user ว่าใครเป็น reviewer

### Step 3: Confirm กับ User

ใช้ AskUserQuestion ถาม user โดยแสดง:
- สรุปไฟล์ที่จะ commit (จาก git status)
- Commit message ที่จะใช้ตาม format ใน CLAUDE.md section 8
- Branch ที่จะ push

<!-- TODO: ใส่ตัวอย่าง commit message ตาม format ของทีม เช่น: -->
<!-- Conventional Commits: `feat(auth): add OAuth2 login flow` -->
<!-- Custom format: `[HZ-147][HZ-142] implement feature X (Reviewed by Name)` -->

### Step 4: ดำเนินการ

เมื่อ user confirm แล้ว:
1. `git add` เฉพาะไฟล์ที่เกี่ยวข้อง (**ไม่ใช้** `git add -A` หรือ `git add .`)
2. `git commit` ด้วย commit message ที่ตกลงกัน
3. `git push` ขึ้น branch ที่ตกลงกัน
4. แสดงผลลัพธ์ให้ user

## Safety Rules

- ห้าม commit ไฟล์ที่มี secrets (`.env`, credentials, API keys)
- ห้าม force push (`--force`, `--force-with-lease`)
- ห้าม push ขึ้น `main` / `master` โดยไม่ได้รับอนุญาตชัดเจน
- ถ้า pre-commit hook fail → แก้ไขปัญหาแล้วสร้าง commit ใหม่ (ห้าม `--no-verify`)
- ถ้ามี uncommitted changes ที่ไม่เกี่ยวข้อง → ถาม user ว่าจะรวมหรือไม่
