<h1 align="center">Photoshop 拖放修复</h1>

<p align="center">
  <img src="./data/images/banner.png" alt="Photoshop 拖放修复 — Windows 3 步诊断 Skill" width="800">
</p>

<p align="center">
  <strong>Windows 11/10 · Adobe Photoshop 2026 (27.x) · 3 步诊断 Skill</strong><br>
  <sub>只诊断不修复 · 不自动执行 · 每一步等用户授权</sub>
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
  <img src="https://img.shields.io/badge/平台-Windows_10%2F11-0078d4?style=flat-square&logo=windows&logoColor=white" alt="平台">
  <img src="https://img.shields.io/badge/兼容-Photoshop_2026_(27.x)-31a8ff?logo=adobephotoshop&logoColor=white&style=flat-square" alt="PS版本">
  <img src="https://img.shields.io/badge/类型-Agent_Skill-001eff?style=flat-square" alt="类型">
  <img src="https://img.shields.io/badge/只诊断-是-success?style=flat-square" alt="诊断模式">
</p>

<p align="center">
  <a href="./README.md">English</a> | <strong>简体中文</strong>
</p>

---

## 🎯 这个 Skill 解决什么

Adobe Photoshop 2026 (27.x) 在 Windows 桌面上突然不能从文件资源管理器拖入文件了?这个 skill 跑一遍 **3 步决策树** 帮你定位根因——**每一步停下等你授权**,绝不自动改注册表、自动重启、自动删文件。

> **为什么只诊断不修复?** Windows + Photoshop 涉及系统级变更(UAC、注册表、进程提权)。操作失误可能波及无关软件。每一步都把"会改什么"摊给你看,等你确认才动。

## ⚡ 快速诊断卡

<table>
  <tr>
    <td width="20%" align="center" valign="middle"><b>🪟 第 1 步</b></td>
    <td width="50%" valign="top"><b>检查 EnableLUA 注册表</b><br>~80% 案例的根因。Microsoft 官方确认 <code>EnableLUA=0</code> 会破坏 Windows 11 拖放。<i>低风险修复:把 <code>0</code> 改成 <code>1</code>,重启 Windows。</i></td>
    <td width="30%" valign="middle" align="center">
      <img src="https://img.shields.io/badge/风险-低-success?style=flat-square" alt="风险"><br>
      <img src="https://img.shields.io/badge/覆盖-80%25-1e88e5?style=flat-square" alt="覆盖率">
    </td>
  </tr>
  <tr>
    <td width="20%" align="center" valign="middle"><b>🛡️ 第 2 步</b></td>
    <td width="50%" valign="top"><b>检查 Photoshop 进程提权</b><br>Adobe 社区验证过的另一根因:Photoshop <i>不能</i> 以管理员身份运行。<i>低风险修复:PS 快捷方式属性里取消勾选"以管理员身份运行"。</i></td>
    <td width="30%" valign="middle" align="center">
      <img src="https://img.shields.io/badge/风险-低-success?style=flat-square" alt="风险"><br>
      <img src="https://img.shields.io/badge/覆盖-+12%25-1e88e5?style=flat-square" alt="覆盖率">
    </td>
  </tr>
  <tr>
    <td width="20%" align="center" valign="middle"><b>🔄 第 3 步</b></td>
    <td width="50%" valign="top"><b>PS 首选项重置 + Explorer 重启</b><br>启动时按 <code>Ctrl+Alt+Shift</code> 重置 PS 首选项 + 重启 Windows 资源管理器。<i>中风险:会清掉 PS 自定义设置,建议先备份。</i></td>
    <td width="30%" valign="middle" align="center">
      <img src="https://img.shields.io/badge/风险-中-orange?style=flat-square" alt="风险"><br>
      <img src="https://img.shields.io/badge/覆盖-+5%25-1e88e5?style=flat-square" alt="覆盖率">
    </td>
  </tr>
</table>

如果前三步全过仍失败,降级到 **Explorer → 记事本 三方拖放测试**,精确区分问题在 Windows 拖放层还是 Photoshop 接收层。

## 📦 适用范围

<table>
<tr><th width="50%">✅ 处理</th><th width="50%">❌ 不处理</th></tr>
<tr><td valign="top">

- Windows 10 / 11 + Photoshop 2026 (27.x) 桌面版
- 文件资源管理器 → PS 画布拖 JPG / PNG / TIFF 没反应
- "昨天还能用,今天突然不行"的场景
- 32 位与 64 位 PS 安装都覆盖

</td><td valign="top">

- macOS(沙箱模型完全不同)
- Illustrator / InDesign / Premiere / After Effects
- 非 Adobe 软件的 Windows 拖放问题
- PS 安装/激活/崩溃/性能问题
- 文件格式不兼容(RAW / HEIF 需装插件)

</td></tr>
</table>

## 🚀 安装

把整个 `photoshop-drag-drop-fix/` 文件夹复制到 skills 目录:

| Agent | 路径 |
|---|---|
| **OpenCode / Codex / 通用** | `~/.agents/skills/photoshop-drag-drop-fix/` |
| **Claude Code** | `~/.claude/skills/photoshop-drag-drop-fix/` |
| **Cursor / 其他** | `~/.opencode/skills/photoshop-drag-drop-fix/` |

下次会话启动时自动加载。

## 🗣️ 触发词

任意一句即激活:

- 「Photoshop 拖不进去」
- 「PS 不能拖文件」
- 「photoshop drag drop 不行」
- 「拖文件到 PS 没反应」
- 「photoshop can't drag」
- English: "Photoshop won't accept drops" / "PS can't drag files" / "photoshop drag drop not working"

## 🧠 设计原则

1. **诊断 ≠ 修复** —— 绝不替你跑 `reg add`、重启电脑、删文件。每一步出结论 + 给修复命令,等你确认才动。
2. **绝不把 `EnableLUA` 改成 0** —— 网络教程常见做法,但 Microsoft 明确禁止——会降低系统安全,且 Windows 11 上反而可能破坏拖放。
3. **从最常见到最冷门** —— 三步顺序对应概率从 80% 递减。允许中途任意一步退出。
4. **明确边界** —— 不修 macOS / 不修其他 Adobe 应用 / 不替你按任何按键。

## 📁 文件结构

```
photoshop-drag-drop-fix/
├── SKILL.md            # agent 看的执行指令
├── README.md           # English documentation
├── README.zh-CN.md     # 本文件
└── LICENSE             # MIT License
```

详细执行步骤见 [SKILL.md](./SKILL.md)。

## ⚠️ 适用范围说明

仅在创建时验证过的环境下测试过。Adobe 后续版本(如 PS 28.x)若修改了拖放接收机制,可能需要适配。如果 Microsoft 变更了 `EnableLUA` 默认值,第 1 步的判定逻辑要重做。

## 🤝 贡献

发现新根因或修复路径?欢迎提 issue / PR。最有帮助的贡献:

- 带 Microsoft / Adobe 官方文档引用 的新根因条目
- SKILL.md(agent 看的执行指令)的其他语言翻译
- 更好的 Photoshop 进程提权检测方法(PowerShell 片段等)

## 📄 License

[MIT](./LICENSE) —— 自由使用、修改、分发、衍生,保留许可证声明即可。

---

## ⭐ Star History

<p align="center">
  <a href="https://star-history.com/#redevilkid-Chan/photoshop-drag-drop-fix&Date">
    <img src="https://api.star-history.com/svg?repos=redevilkid-Chan/photoshop-drag-drop-fix&type=Date" alt="Star History Chart" width="600">
  </a>
</p>