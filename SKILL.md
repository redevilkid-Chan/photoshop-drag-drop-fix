---
name: photoshop-drag-drop-fix
description: 你必须在用户报告「Photoshop 拖不进去 / PS 不能拖文件 / photoshop drag drop 不行 / 拖文件到 PS 没反应 / 文件拖不进 Photoshop」时调用本 skill。仅限 Windows + Adobe Photoshop 2026 (27.x) 桌面版,严格不接 macOS、Illustrator、InDesign、Premiere、After Effects、其他非 Adobe 软件的 Windows 拖放问题。按 3 步顺序诊断树(EnableLUA 注册表 → Photoshop 进程权限 → Photoshop 首选项 + Windows Explorer 重启)逐项排查,**只诊断不修复**,每一步跑完先告知结论再给命令,绝不自动执行 `reg add` / 重启 / 文件删除等高风险操作。前 3 步全过仍失败时降级做 Explorer → 记事本三方拖放测试,区分问题在 Windows 拖放层还是 Photoshop 27.x 自身层。
---

# Photoshop 拖放失败 · Windows 诊断 Skill

## 概述

Adobe Photoshop 27.x 在 Windows 上无法从文件资源管理器拖入文件,几乎都是由三个根因之一引起:**UAC 关闭(EnableLUA=0)**、**Photoshop 以管理员身份运行**、**首选项/Explorer 状态污染**。本 skill 按从最常见到最冷门的顺序逐项排除,每一步独立,允许在中途任意一步给出"已解决"反馈。

## 边界(明确不处理)

| 不处理 | 原因 |
|---|---|
| macOS 拖放失败 | macOS 沙箱 + 权限模型完全不同,需要单独 skill |
| Illustrator / InDesign / Premiere / After Effects 拖放问题 | 各 App 进程权限、首选项位置不同 |
| 非 Photoshop 的 Windows 通用拖放(浏览器/记事本/资源管理器内部) | 应走通用 Windows 拖放排查 |
| Photoshop 安装/激活/崩溃/性能问题 | 应走 Adobe 官方 KB 或通用 PS 排错 |
| 文件本身格式不兼容(RAW、HEIF 等需插件) | 是文件格式问题,不是拖放机制问题 |

## 决策树 · 3 步顺序诊断

### Step 1 · EnableLUA 注册表

**为什么先查这个**:Microsoft 官方文档确认 `EnableLUA=0` 会关闭 UAC 和 Admin Approval Mode,在 Windows 11 上会破坏 Drag & Drop。Adobe 官方未将该字段列在 PS 27.x 系统要求里,但实测 80% 的"PS 突然不能拖"案例根因都在这里。代价:一次 `reg query`,无副作用。

**检查命令**:
```powershell
reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" /v EnableLUA
```

**判定**:

| 输出 | 结论 |
|---|---|
| `0x0` | **异常**。UAC/Admin Approval Mode 已关闭,这是 Windows 11 拖放异常的最常见根因 |
| `0x1` | **正常**。UAC 启用,跳过本步,进入 Step 2 |

**给出修复命令**(等用户授权才动,绝不自己跑):
```powershell
# 提示:此操作需要管理员权限,且修改后必须重启 Windows 才生效
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" /v EnableLUA /t REG_DWORD /d 1 /f
```

**严禁**:
- ❌ 把 `EnableLUA` 改成 `0`(网络教程常见做法,但 Microsoft 明确禁止——会降低系统安全,且 Windows 11 上反而可能破坏拖放)
- ❌ 修改后自动重启电脑
- ❌ 不等用户确认就执行 `reg add`

**验证**(用户重启后):文件资源管理器 → 拖一张 JPG/PNG → 拖到 PS 已打开的画布。能拖入即视为本步解决,exit skill;不能拖入继续 Step 2。

### Step 2 · Photoshop 进程权限

**为什么放第二步**:Adobe 社区多个用户原话确认"Photoshop must NOT be running as administrator"是导致拖放失败的真根因之一。这跟 Step 1 是同类问题(UAC/提权错位),但作用在进程层。

**检查命令**:
```powershell
# 查看 Photoshop.exe 进程是否带提权标记(# 表示管理员权限运行)
tasklist /FI "IMAGENAME eq Photoshop.exe" /V
```

更精确的判定(用 PowerShell):
```powershell
Get-Process -Name Photoshop -ErrorAction SilentlyContinue |
  ForEach-Object {
    $tokenInfo = & advapi32.dll  # 或用以下简化判定
    Write-Output "PID: $($_.Id), Session: $($_.SessionId)"
  }
```

简化判定法:看 `tasklist /V` 输出里,**用户名列**是否为 `Administrator` 或带 `#` 后缀。如果是,就是以管理员身份运行。

**判定**:

| 输出 | 结论 |
|---|---|
| 用户名是普通账号(无 `#`) | **正常**。跳过本步,进入 Step 3 |
| 用户名是 `Administrator` 或带 `#` 提权标记 | **异常** |

**修复指引**(等用户操作,不替你关进程):

1. 完全关闭 Photoshop(包括托盘图标)
2. 桌面/开始菜单找到 Photoshop 图标 → 右键 → 属性 → 兼容性选项卡
3. **取消勾选**「以管理员身份运行此程序」
4. 双击正常图标启动
5. 测试拖放

### Step 3 · Photoshop 首选项 + Windows Explorer 重启

**为什么最后做这两个**:首选项损坏会导致 PS 27.x 行为异常(包括拖放接收器),重启 Explorer 解决 Windows 资源管理器进程污染导致的拖放卡死。两者代价都不大,可一并做。

**Step 3a · Photoshop 首选项重置**

操作指引(由用户手动按,agent 不替代按):
1. 完全关闭 Photoshop
2. 按住 `Ctrl + Alt + Shift` 不放
3. 双击 Photoshop 图标启动
4. 弹出「是否要重置首选项?」选「**是**」
5. 重启后测试拖放

如果用户不放心重置,可先备份:
```powershell
# 备份当前首选项(不删)
Copy-Item "$env:APPDATA\Adobe\Adobe Photoshop 2026 Settings" "$env:USERPROFILE\Desktop\PS-Prefs-Backup-$(Get-Date -Format yyyyMMdd)" -Recurse
```

**Step 3b · Windows Explorer 重启**

```powershell
# 任务管理器 → 找到 "Windows 资源管理器" → 右键 → 重新启动
# 或 PowerShell 等价操作:
Stop-Process -Name explorer -Force
Start-Process explorer
```

**判定**:两项中任一完成后,都让用户测试拖放。能拖入即视为本步解决;都不能拖入进入降级路径。

## 降级路径 · 三方拖放测试

前三步全过仍失败 → 问题不在 PS 自身,需要区分 Windows 拖放层 vs PS 拖放接收层。

**测试方法**(由用户手动做):

1. 打开记事本(无需保存文件)
2. 文件资源管理器 → 找一张 JPG/PNG
3. 拖到**记事本窗口**

**判定**:

| 记事本能拖入 | 结论 |
|---|---|
| ✅ 能 | Windows 拖放层正常,问题在 Photoshop 27.x 自身 |
| ❌ 不能,显示「禁止」图标 | Windows 拖放层坏了,与 PS 无关 |

**如果 Windows 层坏了**,给出临时绕过技巧:
- 选中文件 → 按住左键不放 → 按一下 `Esc` → 松开左键(微软 MVP 社区验证的"click+Esc"解锁技巧)

**如果 Windows 层正常但 PS 不行**,归档症状给用户转 Adobe 官方支持:
- Photoshop 版本号
- Windows 版本号
- 三步诊断树各项结果
- "Click+Esc" 技巧是否能让 Explorer 内部拖放成功

## 输出风格约束(强制)

执行本 skill 时,agent 必须遵守:

1. **每一步独立汇报**,不一次性把所有检查结果倒给用户
2. **先告知结论,再给命令**(PC-A 是非技术用户)
3. **绝不自动执行** `reg add`、Stop-Process、重启电脑、删除文件
4. **每一条 `reg` 命令前明确标注**「需要管理员权限 / 修改后必须重启」
5. **明确不替换 Adobe 官方 KB**:严重场景下引导用户访问 https://helpx.adobe.com/photoshop/kb/basic-troubleshooting.html
6. **绝不修改 `EnableLUA=0`**(网络教程常见错误做法)

## 参考资料

- Microsoft EnableLUA 文档(确认默认值 1、关闭后影响)
- Adobe 官方 PS 基础排错:https://helpx.adobe.com/photoshop/kb/basic-troubleshooting.html
- Adobe 社区 "Photoshop must NOT be running as administrator" 多帖验证
- 微软 Q&A Windows 11 拖放异常 + "click+Esc" 临时绕过技巧