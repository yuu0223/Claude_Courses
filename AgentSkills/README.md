# Agent Skills
---
## Outline
- About Agent Skills
- 

---
## About Agent Skills
### What are Agent Skills?
What: Agent Skills 是一個可以重複使用的 Markdown 文件，它能教導 Claude Code 如何處理特定的任務。
How: 透過 Markdown 文件定義出屬於專案的 Skills，只需要編寫一次，Claude Code 就能在每次遇到特定的類似任務自動套用。
Markdown 中必須包含 name 和 description，如下：
```markdown
---
name: check-pr
description: Reviews Pull Requests for code quality. Use when reviewing PRs or checking code changes.
```
