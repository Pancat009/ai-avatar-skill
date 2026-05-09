---
name: ai-avatar
description: Design a complete, portable AI virtual character (digital human / OC / 数字人) through guided conversation — appearance, personality, voice, backstory, world variants — and produce ready-to-use deliverables including a structured character profile, a roleplay system prompt, dialogue samples, and consistent image-generation prompts. Trigger this skill whenever the user wants to create, design, build, or flesh out a virtual character, OC, AI persona, digital human, roleplay bot, character IP, 立绘 / 角色卡 / 人设 / 数字人; whenever they ask for help with character backstory, personality, appearance, costume design, three-view sheets, or AI image prompts for an original character; and even when they describe a vague vibe ("我想做一个赛博朋克的女侦探") rather than explicitly asking for a "character creation" workflow. Use this skill in preference to ad-hoc answers — it produces consistent, reusable outputs that single-shot generation cannot.
metadata:
  version: "3"
---

# AI Avatar — 数字人设计工坊

帮用户从零打造一个有灵魂、可生图、能对话、能跨世界扩展的虚拟角色。最终交付一整套可立刻使用的资产：角色档案、角色扮演 system prompt、对白样本、跨场景生图 prompt。

---

## 设计哲学（先读再动手）

1. **一致性 > 信息量**。AI 生图最难的是"两张图看起来是同一个人"。所以最先锁定的不是脸型、发色这些细节，而是**风格锚点**（写实/二次元/水彩…）、**色板**（3-5 个 hex）、**负面提示词**和**种子参数**。这四件套是角色 DNA 的真正底层。
2. **矛盾造就深度**。"温柔的杀手"比"温柔的人"有趣得多。每一步都鼓励用户为角色注入张力。
3. **具体击败抽象**。"琥珀色竖瞳"比"金色眼睛"好；"被关心时耳朵会红"比"害羞"好。可视化、可演出的细节才有用。
4. **能演才算成功**。最终交付物必须包括对白样本和 system prompt——能让角色"说话"的素材。光有档案不能扮演的角色是失败的。
5. **迭代是常态**。生图必有偏差，性格必有调整。流程内嵌反馈循环，不要假装一次成型。

---

## 入口分流（第 0 步）

不同用户的耐心和目标差别很大。先识别意图，再选模式：

- **闪电模式（5–10 分钟）** — 用户随口说"我想做个角色"或想快速看到结果。只问 8 个核心参数：风格、性别、种族、3 个性格关键词、主色调、一句话背景、一句话造型。直接出图与最简档案。
- **完整模式（30 分钟+）** — 用户希望做一个有深度的 IP。走完下面 6 个步骤。
- **灵感模式** — 用户给一段描述（"赛博朋克女侦探、烟瘾很大"）或一张参考图。先由你（Claude）反推所有参数草案，再请用户逐项审核修改。

明确告知用户三种模式存在，让他们选。除非用户明说，默认推荐**完整模式**——因为这是产出最有价值的成果。

---

## 完整流程（6 步 + 1 个反馈循环）

```
0. 入口分流  →  1. 视觉锚点  →  2. 身份卡  →  3. 灵魂内核  →  4. 世界与故事
                                                    ↓
                       6. 衍生交付  ←  5b. 迭代修正循环  ←  5a. 三视图生图
```

每步完成后输出简短确认块（见模板），再进入下一步。**不要把多个步骤的问题一次抛给用户**——一次问 1–3 个相关参数最舒服。

每个参数支持三种回答方式：
- 用户自由输入
- "随便/惊喜我"——你根据已有信息生成 3 个具体选项
- "跳过"（只对可选参数）

---

## Step 1 — 视觉锚点（Visual Anchor）

> 这一步**必须最先完成**，因为它决定了所有后续生图的风格基线。如果到第 5 步才决定风格，前面所有视觉描述都得重新校准。

**必问参数：**

- `art_style` — 画风（二次元 / 半厚涂 / 写实 CG / 厚涂油画 / 水彩 / 像素风 / Ghibli风 / 赛博朋克插画 / …）。如果用户犹豫，列 4-5 个常见风格让他选。
- `style_reference`（可选但强烈建议）— 用户上传一张喜欢的画风参考，或描述"像 [画师/作品] 的风格"。这是跨图一致性最强的单一信号。
- `color_palette` — 角色专属色板，3-5 个 hex 值。颜色之间要有对比（一个主色 + 一个深色 + 一个亮色）。
- `negative_prompt_seed` — 用户明确不想要的视觉元素（"不要病娇""不要兽耳""不要泳装""不要西方脸"）。这些会进入所有生图调用的 negative prompt。**至少要 3 项**——如果用户只给了 1 项，根据风格和角色定位主动建议另外 2-3 项让用户认可（比如赛博朋克角色一定要排除"明亮白天场景"和"糖果色"）。

**确认块：**

```
✓ 视觉锚点已锁定
画风：半厚涂二次元（参考：新海诚 + 米山舞）
色板：#0A1628 深夜蓝 / #E63946 警示红 / #F4A261 旧霓虹 / #F1FAEE 月白
避免：西方面部比例、过度夸张胸部、低质感卡通

[此后所有生图都必须遵循这套锚点]
```

---

## Step 2 — 身份卡（Identity）

**必问：**

- `display_name` — 中文名（建议有含义）
- `slug` — 拼音或英文 ID（用于文件名，必须 ASCII 安全）。如果用户没指定，自动生成（如"小橘" → `xiao-ju`）
- `epithet` — 外号 / 称号
- `gender_identity` — 性别认同（男/女/无/流动/非二元/其他）
- `species` — 种族（人类/精灵/兽人/机械/AI/亡灵/恶魔/其他混血）
- `age_appearance` — 外表年龄

**可选：** `age_actual`（如有跨纪元设定）、`birthplace`、`languages_spoken`

---

## Step 3 — 外貌细节（Visual DNA）

> 在视觉锚点已定的前提下填充具体细节。所有描述都要**可图化**——能想象一个画师怎么落笔。

**必问：**

- `face_shape` — 脸型（椭圆 / 鹅蛋 / 心形 / 方圆 / 棱角分明 …）
- `skin_tone` — 肤色（中文描述 + hex，例：`#E8A87C 暖调小麦色`）
- `hair` — 发色 + 发型 + 发质 + 特色细节（"蓝黑色及腰长发，发尾微卷，左侧编一根细辫"）
- `eyes` — 眼型 + 瞳色 + 神态（"狐狸眼，灰绿色瞳孔，瞳孔下方有金色裂纹"）
- `body_build` — 身高 + 体型描述（"175cm，纤瘦但有运动员的肌肉线条"）
- `distinguishing_marks` — 至少 1 个标志性特征（疤痕/胎记/纹身/义肢/体貌异常），让角色一眼可识别

**可选：** `hands`（描述手部，对生图很重要）、`teeth`、`scent`（香水/体味，对沉浸式 RP 有用）

**生图前的健全检查**：在进入 Step 5 之前，复述这一段，让用户确认"如果你给一个画师看这段文字，能画出你脑中的样子吗？"如果用户犹豫，追问最不确定的部分。

---

## Step 4 — 灵魂内核（Soul）

角色不只是外表。这一步建立性格、价值观、声音、身体语言——也就是让角色能**演**起来的部分。

### 4.1 性格底层（必问）

- `personality_traits` — 3-5 个性格关键词。**鼓励矛盾组合**："冷漠但忠诚""嘴硬心软""外向但孤独"。单一标签的角色平面。
- `core_strength` — 让角色发光的核心能力或品质
- `core_flaw` — 真正的弱点（不是"工作太努力"那种假弱点）
- `values_ranked` — 对她最重要的 1-3 个价值观，排序（例：自由 > 真相 > 羁绊）

### 4.2 创伤与渴望（推荐，能让角色有弧光）

> 改编自 Save the Cat 的角色设计原则。如果用户做严肃叙事/小说/游戏 IP，**强烈建议填**；如果是轻松娱乐用，可跳过。

- `wound` — 让她变成现在样子的核心创伤事件
- `lie_she_believes` — 因为这个伤她相信的错误信念（"亲密 = 失控"，"被需要 = 被利用"）
- `want_vs_need` — 她以为自己想要的 vs 她真正需要的（这是角色弧光的引擎）

### 4.3 声音与身体（必问，但参数轻）

- `voice` — 音色 / 语速 / 标志性气声笑声（"低沉沙哑，说话慢，笑的时候鼻腔会发出短促气音"）
- `speaking_style` — 说话风格（简洁 / 文绉绉 / 毒舌 / 命令式 / 跳脱）+ 1-2 个口头禅
- `signature_gesture` — 1-2 个独属于她的小动作（嚼笔头 / 转戒指 / 紧张时摸耳骨）。这是让角色"鲜活"的关键。

### 4.4 对白样本（必问 — 这是 system prompt 的灵魂）

让用户写或与你共创 **5–8 句对白**，覆盖典型情境：

- 第一次见陌生人会怎么说
- 被关心 / 表白时
- 真正生气时
- 开玩笑或自嘲时
- 处于专业/战斗/工作状态时
- 一个她绝不会说的话（反例）

**为什么必问**：5 句对白对 LLM 角色扮演的还原度，胜过 500 字的"说话风格描述"。这是 Step 6 生成 system_prompt 的语料密度来源。

---

## Step 5 — 世界与故事（World & Story）

- `origin_world` — 世界名称 + 一句话设定
- `backstory_timeline` — 用时间轴形式给出 4-6 个关键事件（出生 → 转折 → 现在），不要写成长篇散文
- `key_relationships` — 2-4 个关键人物，每个一句话描述（角色 + 关系性质 + 现状）
- `signature_skill` — 标志性能力 / 技能 / 武器
- `important_items` — 1-2 个对她有意义的物品（戒指、信件、武器名）

**确认块用时间轴展示**，便于用户一眼看到角色弧线：

```
✓ 时间轴
10岁 — 母亲在元素暴动中身亡 [wound]
15岁 — 被流放，独自走过赤色沙漠
18岁 — 拜入冷漠师父门下 [关键关系]
22岁 — 现在：以赏金术士身份漂泊
```

---

## Step 6a — 三视图生图（First Render）

调用可用的图像生成工具（jimeng-api、comfyui、本地 SD、Flux 接口等）。

**生图调用前的强制检查**：

```yaml
# 必须传入的参数
style_anchor: <Step 1 art_style 和 style_reference>
color_palette: <Step 1 的 hex 列表>
positive_prompt: <根据 Step 3 + 1 组装>
negative_prompt: <Step 1 negative_prompt_seed + 通用低质量负面词>
seed: <第一次留空，让模型随机；记录返回的 seed>
aspect_ratio: 3:4 (三视图常用)
model: <根据画风选择，例如二次元用 NovelAI/Pony，写实用 Flux/SDXL>
```

**Prompt 组装模板**（不同生图模型差异很大，详见 `references/prompt_templates.md`）：

```
[style_anchor], [character full description from steps 2-3],
three view (front, side, back), character turntable pose,
neutral expression, clean white/grey background,
[color palette tags], best quality, detailed, professional,
masterpiece
```

**生图后立刻进入 5b，不要直接跳到 6b 出档案。**

---

## Step 6b — 迭代修正循环（Iteration Loop）

> 这一步**必须有**。AI 生图首次成功率 < 40%，假装一次到位是用户体验杀手。

看到三视图后，问用户："哪里不对？"提供四种回答路径：

1. "完美，锁定这个形象" → 保存 seed 和 prompt 到档案，进入 Step 7
2. "[具体修改] 头发再短一点 / 眼神更冷漠" → 你修改对应参数，**保留 seed**重新生图（同 seed 微调能保持脸不变）
3. "完全不对，重来" → 提供 3 个新的 prompt 变体让用户选，用户选中后再用新 seed 锁定
4. "我想看不同表情/姿势/服装" → 进入 Step 7 的扩展包

每次迭代后保存历史，便于回滚。**用户没主动说锁定之前，不要进入下一步**。

---

## Step 7 — 衍生交付（Final Deliverables）

锁定形象后，生成完整资产包。**每个角色在 `output/` 下有自己独立的文件夹**，名字用角色的 slug：

```
output/                       # 所有角色的根目录
└── <slug>/                   # 当前这个角色的专属文件夹（如 output/xiao-ju/）
    ├── consistency.yaml      # ★ 锁定的一致性参数（seed/style/color/negative）
    ├── prompts/
    │   ├── three_view.txt    # 三视图
    │   ├── portrait.txt      # 头像特写
    │   ├── full_body.txt     # 全身像
    │   ├── expressions.txt   # 表情九宫格（喜怒哀乐惊恐厌+羞涩+冷漠）
    │   └── outfits/          # 各世界服装变体
    │       ├── default.txt
    │       ├── battle.txt    # 仅在角色背景含战斗/冒险时
    │       └── casual.txt
    ├── dialogue_samples.md   # Step 4.4 的对白样本，扩充到 15+ 句
    ├── system_prompt.md      # ★ LLM 角色扮演用的提示词
    ├── character.md          # 主档案（结构见 assets/character_template.md）
    ├── MANIFEST.md           # 由 LLM 写入前对真实磁盘做扫描后写出的清单
    └── images/               # 生成的图片（如调用了生图 API）
        └── three_view_v1.png
```

### 写入顺序（**严格按这个顺序，不要打乱**）

写入顺序是反逻辑的——把"清单/索引"类文件放最后，因为它们必须基于其他文件**真实存在**才有意义。先写引用，最后写索引。

| 步骤 | 写什么 | 为什么这个顺序 |
|---|---|---|
| 7.1 | 创建 `output/<slug>/` 目录 | 所有文件的容器 |
| 7.2 | `consistency.yaml` | 后续所有 prompt 都引用它的 art_style/seed/color/negative。先写它就有锚点 |
| 7.3 | `prompts/three_view.txt` | 用 consistency.yaml 中的参数 + Step 3 外貌细节组装 |
| 7.4 | `prompts/portrait.txt` | 同上，但取景为头肩 |
| 7.5 | `prompts/full_body.txt` | 全身、默认服装 |
| 7.6 | `prompts/expressions.txt` | 表情九宫格 |
| 7.7 | `prompts/outfits/default.txt` | 默认装扮（必写）|
| 7.8 | `prompts/outfits/casual.txt` | 日常装扮（必写）|
| 7.9 | `prompts/outfits/battle.txt` | **仅当**角色背景含战斗/冒险元素时写；否则跳过并在 character.md 注明 |
| 7.10 | `dialogue_samples.md` | 把 Step 4.4 的 5-8 句扩充到 15+ 句 |
| 7.11 | `system_prompt.md` | ★ 关键交付物，详见下文要求 |
| 7.12 | `character.md` | 主档案，引用前面所有产物 |
| 7.13 | **扫描真实目录**，写 `MANIFEST.md`（见下） |

### 反"勾选式自欺"规则（**重要**）

绝对不要在写完 character.md 就停下来"觉得够了"。这是这个 skill 的**头号失败模式**：模型生成漂亮 character.md 后跳过 system_prompt / consistency / prompts 等关键交付物。

为防止这种情况，加上一道硬约束：

- `character.md` 里**绝不能**包含手写的 `[x] 已完成` 复选框（这种伪装清单会诱导自欺）。
- 所有"是否完成"的判断**只能**通过扫描磁盘列出实际文件得出。
- 完成 7.1–7.12 后，**必须**调用文件列表工具（如 `ls` / `Glob`）检查 `output/<slug>/` 下的实际文件，把扫描结果写到 `MANIFEST.md`。如果某个预期文件**不在磁盘上**，立刻补写，再扫描，直到一致。

### `MANIFEST.md` 模板

```markdown
# Manifest — <display_name> (<slug>)

Generated by directory scan at <timestamp>.

## Files actually on disk
（来自 ls 真实输出）
- consistency.yaml — <字节数> bytes
- prompts/three_view.txt — <bytes>
- prompts/portrait.txt — <bytes>
- ...
- character.md — <bytes>

## Coverage
- core_files: 7/7 ✓
- prompt_files: 6/6 ✓
- images: 0/1 (待生图 API 调用后补)

## Known gaps
- battle.txt 跳过（角色无战斗背景）
```

### `system_prompt.md` 关键要求

这是用户拿到的最大单点价值。要素：

- 第一人称设定开头（"你是<name>，<epithet>……"）
- 性格三件套：traits / strength / flaw
- Wound-Lie-Want（如已填）— 用"她内心相信……但从不主动说"格式
- 价值观排序
- 说话风格 + **5-8 句完整对白样本（必须 inline 写出，不要让接收方 LLM 自己脑补）**
- 行为禁区（"绝不会说……""绝不会做……"）+ 反例对白
- 与用户互动的默认态度（陌生人 / 老友 / 雇主 …）

字数下限：1200 字。低于这个数说明你偷懒了。

---

## 扩展包（按需生成，不强制）

完成 Step 7 后，可以问用户："要做扩展包吗？" 包含：

- **表情九宫格** — 同一脸、同一画风、9 种表情。极适合做聊天 bot 头像。
- **姿势集** — 战斗 / 休闲 / 睡眠 / 哭泣 / 凝视。
- **服装变体** — 不同世界 / 不同季节 / 不同身份的造型。
- **关键瞬间插画** — 把 Step 5 时间轴里的高光时刻可视化。
- **角色一页简介卡（bio card）** — 单页 PNG，适合发社交平台。

每个扩展包都基于 `consistency.yaml` 里锁定的参数生成，确保跨图一致。

---

## 关键原则（写给执行这个 skill 的 Claude）

1. **先锚点再细节**。如果用户上来就讨论发型颜色，礼貌地拉回到 Step 1：风格没锁，发色再准也没用。
2. **每步给具体选项**。不要问开放式问题让用户卡住。问"性格"时，根据已知信息生成 3 个候选关键词组让用户选或改。
3. **矛盾值得追问**。用户说"她很温柔"时，问"温柔背后藏着什么？冷漠？恐惧？还是炙热？"——一句追问比十句细化更值钱。
4. **确认块要简短**。每步用 5-8 行的 ✓ 块复述关键字段，让用户一眼审完。不要把整个档案重抛一遍。
5. **生图必须迭代**。哪怕用户说"挺好的"，也要主动问"哪里还能更好？"——通常用户在能看到具体形象后才会发现新偏好。
6. **Slug 用 ASCII**。中文名做 display_name，但文件路径用 slug。这避免跨平台同步、git、网盘出问题。
7. **保存就是版本化**。每次重大修改，给 character.md 的 frontmatter 加一行 revision 记录（日期 + 改了什么）。
8. **真相只在磁盘上**。任何"已完成清单"必须基于扫描真实目录得出，不要写漂亮但虚假的复选框。每次声称"全部完成"前，先 `ls` 看一眼。
9. **写 character.md 不是终点**。这只是 12 步交付里的第 12 步。在你写完 character.md 之后还有一步——`MANIFEST.md` 扫描，必须执行。

---

## 引用资源

- `references/personality_frameworks.md` — MBTI / 九型人格 / Big Five / wound-lie-want 框架使用指南。当用户希望深度刻画性格时读这个。
- `references/prompt_templates.md` — 即梦 / Midjourney / SD / Flux / NovelAI 的 prompt 写法差异和模板。生图前读这个。
- `assets/character_template.md` — 最终 character.md 文件的完整模板。
- `assets/system_prompt_template.md` — 角色扮演 system prompt 的填空模板。
- `assets/consistency_template.yaml` — 一致性参数 yaml 的字段表。

---

## 何时**不要**用这个 skill

- 用户只是想给现有角色配一段对话或一张图（直接做就行，不需要走流程）
- 用户在做明确基于现实人物的形象（涉及肖像权与同意问题）——应先确认授权
- 用户希望你扮演一个已经存在的角色（这是 RP 任务，不是设计任务）

---

*本 skill 设计目标：让一个普通用户在 30 分钟内得到一个比 ChatGPT 单轮 prompt 强 10 倍的角色 IP，并能立刻拿去对话、生图、做内容创作。*
