# ai-avatar-skill

> 🌏 [中文文档](README_ZH.md)

A **Claude Code / Agent SDK skill** for designing complete, portable AI virtual characters — OC, digital human, roleplay bot, or character IP — through guided conversation.

**What you get at the end:**
- Structured character profile (`character.md`)
- Roleplay system prompt (ready to paste into any LLM)
- 5+ dialogue samples covering key emotional states
- Three-view image-gen prompts (front / side / back)
- `consistency.yaml` — locks art style, color palette, negative prompts, and seed so every image looks like the same character

> Solves the hardest problem in AI image generation: **making two images look like the same person.**

---

## Install

Clone or download this repo, then place the `ai-avatar/` folder in your Claude skills directory:

**User-level (Claude Code):**
```
~/.claude/skills/ai-avatar/
```

**Project-level:**
```
<your-project>/.claude/skills/ai-avatar/
```

**Windows:**
```
C:\Users\<you>\.claude\skills\ai-avatar\
```

Restart Claude Code or start a new session — the skill is discovered automatically.

---

## Usage

Just describe what you want in plain language. The skill triggers automatically:

```
"I want to design a cyberpunk female detective"
"Help me create a gentle tea-house owner with a secret — ink painting style"
"Build a full character sheet for my novel's protagonist"
"Make an OC, I need three-view sheets too"
```

Claude activates ai-avatar and walks you through the design step by step.

---

## Three Modes

| Mode | Time | Best for |
|------|------|----------|
| **Flash** | 5–10 min | Quick results — only 8 core parameters |
| **Full** | 30 min+ | Serious IP / novel characters — complete 6-step flow |
| **Inspiration** | Varies | Give a vibe or reference image — Claude drafts everything, you review |

---

## Full Flow (6 Steps)

```
0. Mode selection
1. Visual Anchor  (art style / color palette / negative prompts)  ← consistency foundation
2. Identity Card  (name / gender / species / age)
3. Visual DNA     (face / eyes / hair / body / signature marks)
4. Soul Core      (personality / wound / voice / dialogue samples)
5. World & Story  (backstory / timeline / relationships)
6. Deliverables   (three-view prompts + system prompt + multi-scene image prompts)
   └─ built-in iteration loop
```

> **Why Visual Anchor first?** Locking art style, color palette, negative prompts, and seed *before* anything else is the single biggest factor in cross-image consistency. Deciding style at Step 5 means redoing all prior descriptions.

---

## Repository Structure

```
ai-avatar/
├── SKILL.md                          Main skill logic
├── README.md                         This file (English)
├── README_ZH.md                      中文文档
├── LICENSE
├── assets/
│   ├── character_template.md         Character profile template
│   ├── consistency_template.yaml     Visual anchor / consistency lock template
│   └── system_prompt_template.md     Roleplay system prompt template
├── references/
│   ├── personality_frameworks.md     MBTI / Enneagram / Save the Cat reference
│   └── prompt_templates.md           Image-gen prompt patterns + style keyword library
└── evals/
    └── evals.json                    3 evaluation test cases
```

---

## Design Philosophy

1. **Consistency over information** — Lock style/palette/negatives/seed first; fill in face and hair color second
2. **Contradiction creates depth** — "A gentle assassin" is more interesting than "a gentle person"
3. **Specific beats abstract** — "Amber slit pupils" beats "golden eyes"; "ears turn red when cared for" beats "shy"
4. **Must be performable** — Dialogue samples + system prompt are non-negotiable deliverables
5. **Iteration is the norm** — The flow has a built-in feedback loop; one-shot perfection is a myth

---

## Works Well With

- **Image generation**: This skill produces prompts only. Pair with `jimeng-api-skill`, `comfyui`, or `azure-openai-image-skill` for actual generation
- **Story writing**: After character creation, hand off to `story-writer` for plot and narrative

---

## License

MIT — see [LICENSE](LICENSE)

---

## Contributing

Issues and PRs welcome. If you built a character you love using this skill, feel free to share it in the issues.
