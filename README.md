<h1 align="center">Photoshop Drag & Drop Fix</h1>

<p align="center">
  <img src="./data/images/banner.png" alt="Photoshop Drag &amp; Drop Fix — Windows 3-Step Diagnostic Skill" width="800">
</p>

<p align="center">
  <strong>Windows 11/10 · Adobe Photoshop 2026 (27.x) · 3-Step Diagnostic Skill</strong><br>
  <sub>Diagnose-only by design · No auto-fixes · Waits for explicit user authorization</sub>
</p>

<p align="center">
  <a href="https://github.com/redevilkid-Chan/photoshop-drag-drop-fix/stargazers">
    <img src="https://img.shields.io/github/stars/redevilkid-Chan/photoshop-drag-drop-fix?style=flat-square&color=rgb(25%2C%20121%2C%20255)" alt="Stars">
  </a>
  <a href="https://github.com/redevilkid-Chan/photoshop-drag-drop-fix/network/members">
    <img src="https://img.shields.io/github/forks/redevilkid-Chan/photoshop-drag-drop-fix?style=flat-square&color=green" alt="Forks">
  </a>
  <a href="https://github.com/redevilkid-Chan/photoshop-drag-drop-fix/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/redevilkid-Chan/photoshop-drag-drop-fix?style=flat-square&color=blueviolet" alt="License">
  </a>
  <a href="https://github.com/redevilkid-Chan/photoshop-drag-drop-fix/issues">
    <img src="https://img.shields.io/github/issues/redevilkid-Chan/photoshop-drag-drop-fix?style=flat-square&color=orange" alt="Issues">
  </a>
  <img src="https://img.shields.io/badge/Platform-Windows_10%2F11-0078d4?style=flat-square&logo=windows&logoColor=white" alt="Platform">
  <img src="https://img.shields.io/badge/Compatible-Photoshop_2026_(27.x)-31a8ff?logo=adobephotoshop&logoColor=white&style=flat-square" alt="Photoshop">
  <img src="https://img.shields.io/badge/Type-Agent_Skill-001eff?style=flat-square" alt="Type">
  <img src="https://img.shields.io/badge/Diagnose--Only-Yes-success?style=flat-square" alt="Diagnose-Only">
</p>

<p align="center">
  <strong>English</strong> | <a href="./README.zh-CN.md">简体中文</a>
</p>

---

## 🎯 What This Solves

Adobe Photoshop 2026 (27.x) on Windows can suddenly stop accepting drag-and-drop from File Explorer. This skill runs a **3-step decision tree** to find the root cause — and stops at each step to wait for your authorization. **No automatic registry edits, no silent restarts, no file deletions.**

> **Why diagnose-only?** Windows + Photoshop involve system-level changes (UAC, registry, process elevation). Mistakes here can break unrelated apps. Every step shows you exactly what would change and waits for confirmation.

## ⚡ Quick Diagnosis

<table>
  <tr>
    <td width="20%" align="center" valign="middle"><b>🪟 Step 1</b></td>
    <td width="50%" valign="top"><b>EnableLUA Registry Check</b><br>Root cause in ~80% of cases. Microsoft confirms <code>EnableLUA=0</code> breaks Windows 11 drag & drop. <i>Lowest-risk fix: change <code>0</code> → <code>1</code>, restart Windows.</i></td>
    <td width="30%" valign="middle" align="center">
      <img src="https://img.shields.io/badge/Risk-Low-success?style=flat-square" alt="Risk"><br>
      <img src="https://img.shields.io/badge/Coverage-80%25-1e88e5?style=flat-square" alt="Coverage">
    </td>
  </tr>
  <tr>
    <td width="20%" align="center" valign="middle"><b>🛡️ Step 2</b></td>
    <td width="50%" valign="top"><b>Photoshop Process Elevation</b><br>Adobe Community–verified root cause: Photoshop must <i>not</i> run as administrator. <i>Low-risk fix: uncheck "Run as administrator" in PS shortcut properties.</i></td>
    <td width="30%" valign="middle" align="center">
      <img src="https://img.shields.io/badge/Risk-Low-success?style=flat-square" alt="Risk"><br>
      <img src="https://img.shields.io/badge/Coverage-+12%25-1e88e5?style=flat-square" alt="Coverage">
    </td>
  </tr>
  <tr>
    <td width="20%" align="center" valign="middle"><b>🔄 Step 3</b></td>
    <td width="50%" valign="top"><b>Preferences Reset + Explorer Restart</b><br>Reset Photoshop preferences (Ctrl+Alt+Shift on launch) and restart Windows Explorer. <i>Medium-risk: resets PS customizations; backup is recommended first.</i></td>
    <td width="30%" valign="middle" align="center">
      <img src="https://img.shields.io/badge/Risk-Medium-orange?style=flat-square" alt="Risk"><br>
      <img src="https://img.shields.io/badge/Coverage-+5%25-1e88e5?style=flat-square" alt="Coverage">
    </td>
  </tr>
</table>

If all three steps pass and the issue persists, the skill runs a **fallback Explorer → Notepad three-way drag test** to isolate whether the problem is at the Windows drag layer or the Photoshop receiver layer.

## 📦 Scope

<table>
<tr><th width="50%">✅ Handled</th><th width="50%">❌ Out of Scope</th></tr>
<tr><td valign="top">

- Windows 10 / 11 + Photoshop 2026 (27.x) desktop
- Drag JPG / PNG / TIFF from File Explorer → PS canvas fails
- "Suddenly broke" cases (was working yesterday)
- Both 32-bit and 64-bit Photoshop installations

</td><td valign="top">

- macOS (different sandbox model)
- Illustrator / InDesign / Premiere / After Effects
- Non-Adobe apps with broken Windows drag-and-drop
- Photoshop installation / activation / crash / performance issues
- File format incompatibility (RAW / HEIF requiring plugins)

</td></tr>
</table>

## 🚀 Installation

Copy the entire `photoshop-drag-drop-fix/` folder into your skills directory:

| Agent | Path |
|---|---|
| **OpenCode / Codex / general** | `~/.agents/skills/photoshop-drag-drop-fix/` |
| **Claude Code** | `~/.claude/skills/photoshop-drag-drop-fix/` |
| **Cursor / other** | `~/.opencode/skills/photoshop-drag-drop-fix/` |

The skill loads automatically on next session.

## 🗣️ Trigger Phrases

Any of these will activate this skill:

- "Photoshop won't accept drops"
- "PS can't drag files"
- "photoshop drag drop not working"
- "Files dragged to PS don't respond"
- "photoshop can't drag"
- 中文: "Photoshop 拖不进去" / "PS 不能拖文件" / "拖文件到 PS 没反应"

## 🧠 Design Principles

1. **Diagnose ≠ Fix** — Never runs `reg add`, restarts the computer, or deletes files on its own. Each step reports the conclusion and shows the fix command; you confirm before anything runs.
2. **Never sets `EnableLUA` to 0** — Common in web tutorials, but Microsoft explicitly forbids this. It reduces system security AND can break Windows 11 drag & drop.
3. **Most common → most obscure** — Three steps ordered by decreasing probability (80% → ~12% → ~5%). You can exit after any step.
4. **Explicit boundaries** — No macOS fixes, no other Adobe apps, no pressing keys on your behalf.

## 📁 File Structure

```
photoshop-drag-drop-fix/
├── SKILL.md            # Agent-facing execution instructions
├── README.md           # English documentation (this file)
├── README.zh-CN.md     # 中文文档
└── LICENSE             # MIT License
```

For step-by-step execution details, see [SKILL.md](./SKILL.md).

## ⚠️ Scope of Validity

Tested only against the environment verified at skill creation time. Future Adobe versions (e.g. PS 28.x) may change the drag receiver mechanism, requiring skill updates. If Microsoft alters the `EnableLUA` default in future Windows releases, the Step 1 verdict logic must be revisited.

## 🤝 Contributing

Found a new root cause or fix path? Issues and PRs welcome. Common improvements that would help:

- New root cause entries with Microsoft / Adobe documentation references
- Translations of `SKILL.md` (the agent-facing instruction) into additional languages
- Better Process Elevation detection methods (PowerShell snippets, etc.)

## 🔗 Related Work

Three categories of adjacent projects exist; none directly solves "Photoshop can't drag-drop files" on Windows.

### 🔌 Programmatic Photoshop Control (a different problem — agents driving PS)

| Project | What it does | Why it's not us |
|---|---|---|
| [`LissaGreense/photoshop-uxp`](https://github.com/LissaGreense/photoshop-uxp) | Agent Skill that drives PS via UXP scripting | Operates PS *inside*; does not fix drag-drop *into* PS |
| [`00bx/00bx-photoshop-mcp`](https://github.com/00bx/00bx-photoshop-mcp) | Photoshop MCP server, 323 automation tools | Same — automation, not drag-drop repair |
| [`Vaxaxas/photoshop-mcp-windows-first`](https://github.com/Vaxaxas/photoshop-mcp-windows-first) | Windows-first PS MCP | Same |
| [`pangxie231/ps-mcp`](https://github.com/pangxie231/ps-mcp) | Photoshop MCP | Same |

### 🪟 Windows-level Drag-Drop Fixes (different app, same root cause)

These projects fix drag-drop for **other** Windows apps. They share the EnableLUA / admin-elevation root cause but address different surfaces.

| Project | What it fixes |
|---|---|
| [`HerMajestyDrMona/Windows11DragAndDropToTaskbarFix`](https://github.com/HerMajestyDrMona/Windows11DragAndDropToTaskbarFix) | Drag files **to taskbar** in Windows 11 |
| Microsoft Terminal [#17291](https://github.com/microsoft/terminal/issues/17291) | Drag files **to Terminal** when admin (same root cause) |
| Files community [#14498](https://github.com/files-community/Files/issues/14498) | Drag-drop crash in Files app when admin (same root cause) |

### ⚠️ Misleading — Tutorials That Get the Fix Backwards

A widely-shared [cnblogs tutorial (2020)](https://www.cnblogs.com/Chary/articles/14139436.html) recommends **setting `EnableLUA = 0`** to fix this exact problem. Microsoft explicitly warns against this: it reduces system security and can break Windows 11 drag-and-drop in *other* ways. This skill sets `EnableLUA = 1` and explicitly warns against the popular wrong fix. If a tutorial put you at `0`, fix it back to `1` and restart.

### How we differ

| Dimension | This skill | Adjacent projects |
|---|---|---|
| **Scope** | Diagnose only, never auto-fixes | Mostly tools that modify PS or Windows |
| **Approach** | 3 ranked steps with fallback (~80% / +12% / +5%) | Single fix or single tool |
| **Correctness** | `EnableLUA = 1`, explicit warning against `= 0` | Often no direction verification |
| **Trigger** | Auto-runs on phrases like "Photoshop can't drag" | Manual invocation |
| **Installation** | Standalone skill, drag-and-drop into skills folder | Usually bundled inside larger tools |

**Use this skill** when: you want to fix drag-drop on PS (or reproduce the diagnostic for another Windows app).
**Use adjacent projects** when: you want to automate Photoshop work (batch editing, MCP control, scripting).

## 📄 License

[MIT](./LICENSE) — use, modify, distribute, and build on freely while preserving the license notice.

---

## ⭐ Star History

<p align="center">
  <a href="https://star-history.com/#redevilkid-Chan/photoshop-drag-drop-fix&Date">
    <img src="https://api.star-history.com/svg?repos=redevilkid-Chan/photoshop-drag-drop-fix&type=Date" alt="Star History Chart" width="600">
  </a>
</p>