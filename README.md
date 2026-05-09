# ai-avatar — 数字人设计工坊 Skill

一个 Claude Code / Claude Agent SDK 通用的 **Skill**，用来从零打造一个有灵魂、可生图、能对话、能跨世界扩展的虚拟角色（OC / 数字人 / 角色 IP）。

最终交付一整套可立刻使用的资产：
- 结构化角色档案（character.md）
- 角色扮演 system prompt
- 5+ 对白样本
- 三视图 + 跨场景的一致性生图 prompt
- consistency.yaml（锁定画风、色板、负面提示词、种子）

> 解决 AI 生图最难的问题：**两张图看起来是同一个人**。

---

## 安装

将整个 `ai-avatar/` 目录放到你的 Claude skills 目录：

**Claude Code（用户级）：**
```
~/.claude/skills/ai-avatar/
```

**项目级：**
```
<project>/.claude/skills/ai-avatar/
```

Windows 路径示例：
```
C:\Users\<you>\.claude\skills\ai-avatar\
```

重启 Claude Code 或新开会话后，skill 即可被自动发现。

## 使用

直接对 Claude 说出意图即可触发，例如：

- "我想做个角色，赛博朋克风格的女侦探"
- "帮我设计一个温柔但藏着秘密的男茶馆老板，水墨风"
- "给我的小说女主做完整人设"
- "做一个 OC，三视图也要"

Claude 会自动激活 ai-avatar，按对话流程引导你完成设计。

## 三种模式

| 模式 | 用时 | 适合 |
|------|------|------|
| **闪电模式** | 5–10 分钟 | 只想快速看到结果，问 8 个核心参数 |
| **完整模式** | 30 分钟+ | 严肃 IP / 小说人设，6 步全流程 |
| **灵感模式** | 视情况 | 给一句 vibe 或参考图，Claude 反推草案后审核 |

## 6 步流程（完整模式）

```
0. 入口分流
1. 视觉锚点（画风 / 色板 / 负面提示）   ← 一致性的真正底层
2. 身份卡（名字 / 性别 / 种族 / 年龄）
3. 外貌细节（脸 / 眼 / 发 / 体 / 标志性特征）
4. 灵魂内核（性格 / 创伤 / 声音 / 对白样本）
5. 世界与故事（背景 / 时间轴 / 关系网）
6. 衍生交付（三视图 + system prompt + 多场景生图）
   └─ 内嵌迭代修正循环
```

## 目录结构

```
ai-avatar/
├── SKILL.md                          主流程
├── README.md                         本文件
├── LICENSE
├── assets/
│   ├── character_template.md         角色档案模板
│   ├── consistency_template.yaml     一致性锚点模板
│   └── system_prompt_template.md     角色扮演 prompt 模板
├── references/
│   ├── personality_frameworks.md     MBTI / Enneagram / Save the Cat 框架速查
│   └── prompt_templates.md           生图 prompt 写法 + 风格关键词库
└── evals/
    └── evals.json                    3 个评测用例
```

## 设计哲学

1. **一致性 > 信息量** — 先锁画风/色板/负面/种子，后填脸型发色
2. **矛盾造就深度** — "温柔的杀手"比"温柔的人"有趣
3. **具体击败抽象** — "琥珀色竖瞳"比"金色眼睛"好
4. **能演才算成功** — 对白样本 + system prompt 是必交付物
5. **迭代是常态** — 流程内嵌反馈循环

## 与其他 skill 配合

- **生图执行**：本 skill 只产出 prompt，实际生图建议配合 `comfyui` 或 即梦 或 GPT-image 等生图工具或Skill
- **故事扩展**：角色做完后接 `story-writer` 写剧情

## License

MIT — 见 [LICENSE](LICENSE)

## 贡献

欢迎 issue / PR。如果你用本 skill 做出了喜欢的角色，也欢迎在 issue 里晒图。
