# Photoshop 拖放修复 · Windows 诊断工具

Adobe Photoshop 2026 (27.x) 在 Windows 桌面上无法从文件资源管理器拖入文件?这个 skill 按 3 步顺序诊断树帮你定位根因,**只诊断不修复**,每一步等用户授权再动。

## 这个 skill 解决什么

把"Photoshop 突然不能拖文件了"这类问题从随机猜测变成系统排查:
- **第一步**:检查 `EnableLUA` 注册表(80% 案例根因,Microsoft 官方文档确认会破坏 Windows 11 拖放)
- **第二步**:检查 Photoshop 进程是否以管理员身份运行(Adobe 社区验证过的另一根因)
- **第三步**:Photoshop 首选项重置 + Windows Explorer 重启

如果前 3 步全过仍失败,降级到 **Explorer → 记事本** 三方拖放测试,精确区分问题在 Windows 拖放层还是 Photoshop 27.x 自身层。

## 适用场景

- ✅ Windows + Photoshop 2026 (27.x) 桌面版
- ✅ 用户从资源管理器拖 JPG / PNG / TIFF 到 PS 画布没反应
- ❌ macOS(完全不同的沙箱模型)
- ❌ Illustrator / InDesign / Premiere(各自进程权限不同)
- ❌ 非 Adobe 软件的 Windows 拖放问题

## 安装

把整个 `photoshop-drag-drop-fix/` 文件夹复制到你的 skills 目录:

- **Claude Code**:`~/.claude/skills/photoshop-drag-drop-fix/`
- **OpenCode / 其他**:`~/.agents/skills/photoshop-drag-drop-fix/` 或 `~/.opencode/skills/`

agent 下次会自动加载本 skill。

## 触发词

以下表达任意一种即触发:
- "Photoshop 拖不进去"
- "PS 不能拖文件"
- "photoshop drag drop 不行"
- "拖文件到 PS 没反应"
- "photoshop can't drag"

## 设计原则

1. **诊断 ≠ 修复**:不替你执行 `reg add`、重启电脑、删除文件。每一步独立汇报结论 + 给出修复命令,等你确认才动。
2. **绝不把 `EnableLUA` 改成 0**:网络教程常见做法,但 Microsoft 明确禁止——会降低系统安全,且 Windows 11 上反而可能破坏拖放。
3. **从最常见到最冷门**:三步顺序对应概率从 80% 递减,允许中途任意一步退出。
4. **明确边界**:不修 macOS / 不修其他 Adobe 应用 / 不替用户按任何按键。

## 文件结构

```
photoshop-drag-drop-fix/
├── SKILL.md            # agent 看的执行指令(技术细节)
├── README.zh-CN.md     # 本文件
├── README.en.md        # English documentation
└── LICENSE             # MIT License
```

详细执行步骤见 [SKILL.md](./SKILL.md)。

## 已知作用范围

仅适用于本 skill 创建时点验证过的环境。Adobe 后续版本(如 PS 28.x)若修改了拖放接收机制,可能需要更新本 skill。Microsoft 未来若变更 `EnableLUA` 默认值,Step 1 的判定需重做。

## 反馈

发现新根因或修复方式,欢迎提 issue / PR。

## License

MIT