---
name: Bug Report
about: Tell me which step of the diagnostic failed and what you saw
title: "[BUG] <Photoshop version> · <Windows version> · <step>"
labels: ["bug", "needs-triage"]
assignees: []
---

## Help

This skill runs a 3-step decision tree. If any step **misdiagnosed your case** (e.g., skill said "fix EnableLUA" but you fixed it and still can't drag), this is the right template. If the skill worked perfectly and you want a **new root cause** to be added, use **Feature Request** instead.

## Environment

- **Windows version** (e.g., Windows 11 23H2): <!--win-ver-->
- **Photoshop version** (e.g., 2026 v27.0.0): <!--ps-ver-->
- **Photoshop installed via** (Creative Cloud / direct installer / Microsoft Store): <!--install-->

## What broke

- **Which step was run**: Step 1 (EnableLUA) / Step 2 (Process Elevation) / Step 3 (Preferences + Explorer) / Fallback (Explorer → Notepad)
- **The skill's verdict**: <!--verdict-->
- **Your expected verdict**: <!--expected-->

## What I tried

<!--paste the exact commands you ran and their output, plus any manual fix attempts-->

```
<paste terminal output here>
```

## Outcome

- [ ] Fix worked, drag-drop now functional
- [ ] Fix did NOT work, drag-drop still broken
- [ ] Other (describe below)

<!--Additional notes, screenshots, or related info-->

## Checklist

- [ ] I searched [existing issues](https://github.com/redevilkid-Chan/photoshop-drag-drop-fix/issues) and found no duplicate
- [ ] I rebooted Windows after the suggested change (if step 1 was applied)
- [ ] I ran the diagnostic with the agent that hosts this skill (not a different LLM)