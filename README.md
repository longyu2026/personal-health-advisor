# Personal Health Advisor

> A personal health advisor skill for AI agents — covers human symptoms, pet health, lab report interpretation, and medication/diet guidance. Modern medicine first, TCM as supplement, with red-flag emergency safety rules.

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)
![Size](https://img.shields.io/badge/size-8%20files-blue.svg)

## Why this exists

When you feel unwell, you Google it — and either panic or get lost in medical jargon. At the doctor's office, you don't know which department to pick or how to describe symptoms.

This skill encodes the workflow of a **GP + veterinarian + triage nurse**:

1. **Loads your medical history** — no need to repeat "I have reflux, I had an ECG" every time
2. **Red-flag first** — real emergencies get redirected to ER immediately, no analysis
3. **Asks when unsure** — vague symptoms get followed up with targeted questions, no guessing
4. **Fixed output structure** — judgment → reasoning → danger signs → what to do now → which department
5. **Human/pet split** — cats, dogs, reptiles have completely different medication rules

## How it works

```
User says "我胸口有点闷"
         │
         ▼
┌──────────────────┐
│ 1. Identify subject │  human? pet?
└────────┬─────────┘
         ▼
┌──────────────────┐
│ 2. Red-flag check  │  hit? → ER advice immediately
└────────┬─────────┘
         ▼ (no red flag)
┌──────────────────┐
│ 3. Read profile    │  load my-health-profile.md
│    + differential  │  2-3 possible causes
└────────┬─────────┘
         ▼
┌──────────────────┐
│ 4. Fixed output    │  judgment / reasoning /
│                    │  red flags / what to do /
│                    │  which department
└──────────────────┘
```

## Project structure

```
personal-health-advisor/
├── SKILL.md                          # Core: trigger rules + workflow + output template
└── references/
    ├── my-health-profile.md          # Your health record (template, fill in yourself)
    ├── red-flags.md                  # Human + pet emergency red flags
    ├── symptom-frameworks.md         # Symptom differential (chest pain, GI, dizziness...)
    ├── doctor-nav.md                 # Which department, what tests, how to talk to doctor
    ├── animal-health.md             # Cat / dog / reptile common issues
    ├── lab-interpretation.md        # How to read blood work, liver/kidney panels, ECG
    └── med-supplement-guide.md       # OTC meds, supplements, food safety
```

## Quick start

### For AI agent users (Claude Code, Cursor, Doubao, etc.)

1. Clone this repo into your agent's skills directory:
   ```bash
   git clone https://github.com/longyu2026/personal-health-advisor.git
   ```
2. Open `references/my-health-profile.md` and replace all `{placeholders}` with your real info
3. Just tell your agent "我不舒服" / "my cat is vomiting" — it will auto-trigger this skill

### What it looks like

```
【一句话判断】
Most likely: chest wall muscle strain, low risk.

【为什么这么判断】
1. Pain only on deep breath, fixed location
2. No prior cardiac ischemia on ECG
3. Possibly sleeping position last night

【红旗警告】
Go to ER immediately if:
- Persistent chest pain at rest >15 min
- Chest pain with exertion + cold sweat
- Sustained palpitations

【现在可以做什么】
1. Avoid heavy chest expansion
2. Warm compress 10 min
3. Observe 2 days; see doctor if no improvement

【要不要去医院】
- Department: General practice / thoracic
- No special tests needed; physical exam
```

## Design highlights

- **Progressive Disclosure**: SKILL.md stays lean (<7KB). Detailed knowledge lives in 7 reference files loaded on demand.
- **Red-flag safety layer**: `red-flags.md` is a standalone gate. Any hit bypasses analysis and goes straight to ER advice.
- **Profile/logic separation**: `my-health-profile.md` is a blank template. Your personal data never touches the main workflow.
- **Tested with 10 real scenarios**: After building, I ran 10 real user scenarios to find gaps, then added follow-up questions, lab interpretation, and medication guidance.

## Supported pets

- **Cats**: reverse sneezing, vomiting, diarrhea, diet hazards, common emergencies
- **Reptiles/turtles**: shell rot, eye disease, buoyancy issues, pneumonia, environmental causes
- Other pets: the framework adapts — add your species to `animal-health.md`

## Disclaimer

- This is a health advisor, **not a doctor**. All output is for reference only.
- For red-flag symptoms, go to ER immediately.
- For pets, consult a licensed veterinarian. Never feed human medication to animals.

## License

[MIT](LICENSE)
