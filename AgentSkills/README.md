# Agent Skills

## Outline
- About Agent Skills
- 


## About Agent Skills
### What are Agent Skills?
> **What**
- Agent Skills 是一個可以重複使用的 Markdown 文件，它能教導 Claude Code 如何處理特定的任務。通常用於重複性高且可定義出流程的任務。
> **How**
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
> **SKILL.md**
- SKILL.md 由 YAML(Metadata) + Markdown(Instructions) 所組成，若超過 500 行可以考慮將 skill 拆成多個 skills
```
[YAML]
---
name: check-pr
description: Reviews Pull Requests for code quality. Use when reviewing PRs or checking code changes.
---
[Markdown]
# My Skill Name
...
## Instruction
...
```
- 在撰寫 YAML 的時候可以包含以下項目：
  - name(**require**):

    這個 Skill 的名稱
  - description(**require**):

    這個 Skill 的任務描述，描述得越清楚越好
  - allowed-tools(**optional**):

    Agent 在執行任務時無需請求，即可使用這些工具 e.g., READ → 在執行這個 skill 的時候只能讀取檔案，不能編輯。
  - model(**optional**):

    模型選用 e.g., sonnet

> **Agent Skills 層級**
- 當專案在使用 Skills 的時候，會遵照以下的層級來執行。
- e.g., 當 Enterprise 的 Skills 跟 Personal 的命名有衝突時，Claude Code 會選擇使用 Enterprise 的準則
```
Priority for name conflicts: Enterprise → Personal → Project → Plugins

1. Enterprise Path: managed-settings.json
2. Personal Path: ~/.claude/skills/
3. Project Claude Skills: project/.claude/skills
4. Installed Plugins: project/.claude-plugin/plugin.json
```

> **Agent Skills v.s. 其他 Claude tools**
- Claude.md
| Agent Skills | Claude.md |
| ---- | ---- |
| 按需要載入，適合特定任務的專業知識（特定） | 每次都需要載入的知識（通用）e.g., 每次都不要更動到DB內的資料 |

- Subagents
|Agent Skills|Subagents|
|---|---|
|在這次的對話中增添知識|可以在isolated的環境中委派任務|

- Hooks
|Agent Skills|Hooks|
|---|---|
|請求驅動(request-driven)|事件驅動(event-driven) e.g., save file|

> **Agent Skills 如何除錯**
- Skills 未能觸發

→ 請檢查你的描述與實際表達請求的方式是否一致

→ 加入 users 實際會使用的詞彙or關鍵字 e.g.,為什麼這個跑得這麼慢？

- Skills 無法加載

→ 確認路徑、檔名是否都正確 (路徑一定要放在/skill_name/SKILL.md中，檔名一定要是SKILL.md)

→ 運行 ```claude --debug``` 可協助除錯

- Skills 插件功能缺失

→ 清除快取並重新安裝

→ ```rm -/.claude/plugins/cache```

→ ```skills-ref validate [your skill path]```

- Skills Runtime Error

→ ```chmod +x ./check-setup.py```
