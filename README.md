# Context Engineer Template

Template สำเร็จรูปที่ใช้หลักการ **Context Engineering** เพื่อเพิ่มประสิทธิภาพของ AI coding agent ให้สูงสุด Clone template นี้เข้าไปในโปรเจคใดก็ได้ เพื่อให้ AI assistants (Claude Code, Cursor, Copilot ฯลฯ) ได้รับ context ที่มีโครงสร้าง และสามารถ implement ได้สำเร็จตั้งแต่รอบแรก

## Context Engineering คืออะไร?

> *"Context engineering is the art of providing all the context for the task to be plausibly solvable by the LLM."*
> — **Tobi Lutke**, CEO of Shopify

> *"Context engineering is the delicate art and science of filling the context window with just the right information for the next step."*
> — **Andrej Karpathy**

Context Engineering เป็นศาสตร์ที่ก้าวข้ามการทำ prompt engineering แบบเดิม แทนที่จะเขียน prompt เพียงอันเดียว มันมุ่งเน้นการออกแบบ **ระบบที่ dynamic** ซึ่งให้ข้อมูลและเครื่องมือที่ถูกต้อง ในรูปแบบที่ถูกต้อง ในเวลาที่ถูกต้อง เพื่อให้ LLM มีทุกอย่างที่ต้องการในการทำงานให้สำเร็จ

คำนี้ถูกทำให้เป็นที่รู้จักโดย **Tobi Lutke** ในเดือนมิถุนายน 2025 และถูกนำไปใช้อย่างรวดเร็วในชุมชน AI engineering ในฐานะแนวทางมาตรฐานสำหรับการพัฒนาซอฟต์แวร์ด้วย AI

### หลักการสำคัญ

- **ระบบ ไม่ใช่แค่ข้อความ** — Context ไม่ใช่ static prompt แต่เป็นระบบ dynamic ที่ทำงานก่อนทุกการเรียก LLM
- **ข้อมูลที่ถูกต้อง ในเวลาที่ถูกต้อง** — โมเดลได้รับเฉพาะความรู้และเครื่องมือที่เกี่ยวข้องกับงานปัจจุบัน
- **รูปแบบสำคัญ** — Context ที่มีโครงสร้างและ annotation ให้ผลดีกว่าการยัดข้อมูลดิบ
- **ตัวอย่างดีกว่าคำสั่ง** — การแสดง code pattern จริงได้ผลดีกว่าการอธิบายด้วยคำพูด

## มีอะไรอยู่ใน Template นี้?

```
context-engineer-template/
├── CLAUDE.md                          # คำสั่งสำหรับ AI agent ของโปรเจค
├── INITIAL.md                         # Template สำหรับ feature request (4 sections)
├── examples/                          # ตัวอย่าง code พร้อม annotation
│   └── README.md                      # คู่มือการเพิ่มตัวอย่าง
├── PRPs/                              # Product Requirement Plans
│   ├── templates/
│   │   └── PRP-TEMPLATE.md            # Template สำหรับ PRP (6 sections)
│   ├── active/                        # PRP ที่กำลังดำเนินการ
│   └── README.md                      # คู่มือ workflow ของ PRP
└── .claude/
    ├── commands/
    │   ├── generate-prp.md            # /generate-prp — สร้าง PRP จาก feature request
    │   ├── execute-prp.md             # /execute-prp — Implement PRP ทีละขั้นตอน
    │   ├── quality-check.md           # /quality-check — รัน quality pipeline ทั้งหมด
    │   └── push.md                    # /push — Stage, commit & push ตาม convention
    └── settings.json                  # สิทธิ์การใช้งาน Claude Code
```

### ส่วนประกอบ

| ส่วนประกอบ | หน้าที่ |
|-----------|---------|
| **CLAUDE.md** | คำสั่งหลักของโปรเจค — tech stack, conventions, architecture, gotchas AI agent อ่านไฟล์นี้ก่อน |
| **INITIAL.md** | Template สำหรับ feature request แบบมีโครงสร้าง ประกอบด้วย 4 sections: FEATURE, EXAMPLES, DOCUMENTATION, OTHER CONSIDERATIONS |
| **examples/** | Code snippets พร้อม annotation ที่คัดลอกจาก codebase จริง AI อ่านก่อนสร้าง code ใหม่ |
| **PRPs/** | Product Requirement Plans — เอกสาร context ที่ครบถ้วน ช่วยให้ implement feature ใหม่สำเร็จใน pass เดียว |
| **Slash Commands** | Workflow สำเร็จรูป: `/generate-prp`, `/execute-prp`, `/quality-check`, `/push` |

## เริ่มต้นใช้งาน

1. **คัดลอก template นี้** ไปไว้ที่ root ของโปรเจค
2. **กรอก CLAUDE.md** — แทนที่ `{placeholders}` ทั้งหมดด้วย tech stack, conventions, และ architecture จริงของโปรเจค
3. **เพิ่ม examples/** — คัดลอก code จาก codebase จริงมาพร้อม annotation เป็น reference patterns
4. **ใช้ workflow:**
   - เขียน feature request ใน `INITIAL.md`
   - รัน `/generate-prp` เพื่อสร้าง PRP ที่ครบถ้วน
   - รัน `/execute-prp` เพื่อ implement ด้วย context เต็มรูปแบบ
   - รัน `/quality-check` เพื่อตรวจสอบคุณภาพ

## PRP Workflow

```
INITIAL.md → /generate-prp → PRPs/active/{feature}.md → /execute-prp → Implementation
```

PRP แต่ละฉบับประกอบด้วย 6 sections ที่ออกแบบมาเพื่อเพิ่มโอกาสสำเร็จของ AI implementation:

1. **Goal & Why** — สิ่งที่ต้องสร้างและ acceptance criteria
2. **Context Requirements** — ไฟล์ที่ต้องอ่าน, docs, library quirks
3. **Implementation Blueprint** — Data models, รายการ tasks, จุดเชื่อมต่อ
4. **Validation Loop** — Lint, test, และ integration gates
5. **Anti-Patterns** — สิ่งที่ต้องหลีกเลี่ยงเฉพาะ feature นี้
6. **Completion Checklist** — เกณฑ์ความสำเร็จ

ทุก PRP มี **Confidence Score (1-10)** — ควร execute เมื่อ score >= 7 เท่านั้น

## ทำไมถึงได้ผล

การเขียน code ด้วย AI แบบเดิมมักล้มเหลว เพราะโมเดลขาด context เกี่ยวกับ conventions, patterns, และ gotchas ของโปรเจค Context Engineering แก้ปัญหานี้ด้วย:

- **ลด hallucination** — AI เห็นตัวอย่างจริงจาก codebase ไม่ใช่ patterns ทั่วไป
- **บังคับความสม่ำเสมอ** — Conventions ถูกบันทึกไว้ที่เดียว ใช้ได้ทุกที่
- **สำเร็จใน pass เดียว** — PRP โหลด context ทั้งหมดล่วงหน้า AI ไม่ต้องเดา
- **จับ edge cases ตั้งแต่เนิ่น ๆ** — Gotchas และ anti-patterns ถูกระบุไว้ชัดเจน

## แหล่งอ้างอิงและอ่านเพิ่มเติม

- [The New Skill in AI is Not Prompting, It's Context Engineering](https://www.philschmid.de/context-engineering) — Philipp Schmid
- [The Rise of Context Engineering](https://blog.langchain.com/the-rise-of-context-engineering/) — LangChain Blog
- [Context Engineering Guide](https://www.promptingguide.ai/guides/context-engineering-guide) — Prompt Engineering Guide
- [Context Engineering in Agents](https://docs.langchain.com/oss/python/langchain/context-engineering) — LangChain Docs

### Credits

แนวคิด **Context Engineering** ถูกทำให้เป็นที่รู้จักโดย **Tobi Lutke** (CEO, Shopify) ในเดือนมิถุนายน 2025 โดยมีส่วนร่วมสำคัญจาก **Andrej Karpathy** และชุมชน AI engineering ที่กว้างขึ้น รวมถึง **Philipp Schmid**, **Ankur Goyal**, **Dex Horthy**, และ **Cole Medin** — ผู้สร้าง tooling และ methodology เชิงปฏิบัติสำหรับ AI coding agents (CLAUDE.md, PRPs, examples folders, slash commands)

## License

Template นี้ใช้งานได้ฟรี ปรับแต่งได้ตามความต้องการของโปรเจค
