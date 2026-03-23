# Agent Skills

## Outline
- About Agent Skills
- 


## About Agent Skills
### What are Agent Skills?
> What
- Agent Skills 是一個可以重複使用的 Markdown 文件，它能教導 Claude Code 如何處理特定的任務。
> How
- 透過 Markdown 文件定義出屬於專案的 Skills，只需要編寫一次，Claude Code 就能在每次遇到特定的類似任務自動套用。
- 每個 Skills 都會創建一個屬於自己的 folder 和 SKILL.md，並且存放在 ```~/.claude/skills``` 路徑底下
```
~/.claude/skills/
├── check-pr/
│   └── SKILL.md
├── save_file/
│   ├── SKILL.md
│   └── scripts/
│       └── helper.py
└── another-skill/
    ├── SKILL.md
    └── references/
```
- SKILL.md 由 YAML(metadata) + Markdown(Instructions) 所組成
```markdown
[YAML]
---
name: check-pr
description: Reviews Pull Requests for code quality. Use when reviewing PRs or checking code changes.
---
[Markdowns]
# My Skill Name
...
## Instruction
...
```

