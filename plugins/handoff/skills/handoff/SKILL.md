---
name: handoff
description: Use when the user wants to save a compact handoff file for a new AI session so the next session can understand the current context before taking action.
---

# Handoff

## Purpose

Generate a compact handoff file for a new AI session. Preserve current context, decisions, constraints, progress, verification, and next steps without carrying the full chat history.

## Behavior

- Write to `cwd/_docs/handoff/<topic>-YYYYMMDD-HHMMSS.md`.
- Use a readable, filesystem-safe topic: about 10 Chinese characters or 3-6 English words; remove spaces and punctuation; use `handoff` if unclear.
- Use the user's language by default.
- Keep the file compact but complete; prefer precise bullets.
- Do not invent context. Mark unknowns as `Unknown` or `None known`.
- Separate confirmed facts, assumptions, open questions, and recommendations.
- Do not inspect the repository unless explicitly asked, essential facts are missing and local inspection can recover them, or Git anchors are required.
- If inside Git, collect `git rev-parse HEAD`, `git branch --show-current`, `git status --short`, and current date/time. Record clean/dirty; use `Unknown` when unavailable. Do not paste full diffs.
- Omit sensitive values, secrets, tokens, and personal data; say only that sensitive material was present and must be re-supplied securely if needed.
- After writing, output only the absolute file path and this instruction: “请只读读取这个文件并复述上下文；除此之外，在用户确认前不要修改文件、运行命令、调用工具或执行任何推进动作。”

## Required file structure

```markdown
---
Anchor-Commit: ...
Anchor-Branch: ...
Worktree-Status: clean | dirty | Unknown
Created-At: ...
---

请接手下面这个已经进行过一段时间的任务。你的第一步只是理解上下文并复述。允许只读读取本交接文件；除此之外，在用户确认前不要修改文件、运行命令、调用工具或执行任何推进动作。

## 当前目标
- ...

## 成功标准
- ...

## 用户明确要求 / 偏好
- ...

## 已确认上下文
- ...

## 已完成工作
- ...

## 当前状态
- ...

## 验证命令 / 结果
- 已运行：...
- 结果：...
- 未运行 / 待验证：...

## 现实校准 / Git Anchor
- 本交接基于提交：...
- 本交接生成时分支：...
- 本交接生成时工作区状态：...
- 用户确认继续后，先运行 `git status --short`。
- 若 Anchor-Commit 不为 Unknown 且当前提交不同，先查看 `git diff --stat <Anchor-Commit>`；只读取本任务相关文件的 scoped diff 或真实内容。

## 相关文件 / 目录 / 工具
- ...

## 已做决策
- ...

## 不要重复的尝试
- ...

## 未决问题
- ...

## 建议下一步
1. ...
2. ...
3. ...

## 给新会话的要求
- 先只读读取本交接文件并简短复述理解。
- 用户确认前不要修改文件、运行命令、调用工具或推进任务。
- 用户确认后先校验 Git 状态和关键文件；以真实代码和 Git diff 为准。
- 区分事实、假设和建议，不扩大范围。
```

## Quality checks

Before responding, ensure the saved file is readable as the new session's first context source, verification clearly distinguishes run/not-run/unknown, no unsupported claims are included, Git anchors are present when available, and recommended next steps are actionable and gated behind user confirmation.
