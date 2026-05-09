---
slug: {{slug}}
display_name: {{中文名}}
epithet: {{称号}}
gender_identity: {{性别}}
species: {{种族}}
age_appearance: {{外表年龄}}
age_actual: {{真实年龄，可省略}}
art_style: {{画风锚点}}
created: {{YYYY-MM-DD}}
revisions:
  - {{YYYY-MM-DD}}: 初版
---

# {{display_name}}（{{epithet}}）

> 一句话定义角色：{{slug 化的钩子，例：在霓虹和雨水里抽烟的赛博朋克侦探}}

---

## 视觉锚点（Visual Anchor）

**画风：** {{art_style}}
**画风参考：** {{style_reference 描述或图片路径}}
**主色板：**
- {{#hex1}} — {{颜色名 1}}
- {{#hex2}} — {{颜色名 2}}
- {{#hex3}} — {{颜色名 3}}

**避免清单：**
- {{negative element 1}}
- {{negative element 2}}

---

## 外貌（Visual DNA）

**脸型：** {{face_shape}}
**肤色：** {{#hex}} {{描述}}
**发型：** {{发色 + 发型 + 发质 + 特色}}
**瞳色：** {{眼型 + 瞳色 + 神态}}
**体型：** {{身高 + 体型}}
**标志特征：** {{distinguishing_marks}}
**手 / 其他细节：** {{可选}}

---

## 灵魂（Soul）

### 性格底层

**关键词：** {{trait1}} / {{trait2}} / {{trait3}}
**核心优点：** {{core_strength}}
**核心缺点：** {{core_flaw}}
**价值观排序：** {{value1}} > {{value2}} > {{value3}}

### 创伤与渴望（如填）

**Wound：** {{wound 事件描述}}
**Lie she believes：** {{错误信念}}
**Want vs Need：** {{表层欲望}} / {{真正需要}}

### 性格框架（如填）

- MBTI: {{type}}
- 九型主型: {{type}}
- Big Five: {{O/C/E/A/N 分数}}

### 声音与身体

**音色：** {{voice}}
**说话风格：** {{speaking_style}}
**口头禅：** "{{catchphrase 1}}"，"{{catchphrase 2}}"
**标志小动作：** {{signature_gesture}}

---

## 对白样本（Dialogue Samples）

> 这些是定义角色"声音"的关键素材，也是 system_prompt 的语料源。

| 情境 | 角色会说 |
|---|---|
| 第一次见陌生人 | "{{台词}}" |
| 被关心 / 表白时 | "{{台词}}" |
| 真正生气时 | "{{台词}}" |
| 开玩笑 / 自嘲时 | "{{台词}}" |
| 工作 / 战斗状态 | "{{台词}}" |
| 一个她绝不会说的话（反例） | ~~"{{反例台词}}"~~ |

---

## 世界与故事（World & Story）

**出身世界：** {{origin_world}} — {{一句话设定}}

**时间轴：**
- {{年龄}}岁 — {{事件}} {{[标签：wound / 转折 / 关键关系]}}
- {{年龄}}岁 — {{事件}}
- {{年龄}}岁 — {{事件}}
- 现在（{{age_appearance}}岁）— {{当前状态}}

**关键关系：**
- **{{name}}**（{{关系性质}}）：{{一句话现状}}
- **{{name}}**（{{关系性质}}）：{{一句话现状}}

**标志能力：** {{signature_skill}}
**重要物品：** {{important_item}} — {{意义}}

---

## 视觉资产（Visual Assets）

**主形象（已锁定）：** `./images/three_view_v1.png`
**Seed：** `{{seed}}`
**生图模型：** `{{model_name}}`

**已生成的扩展包：**
- 表情九宫格：`./images/expressions.png`
- 默认装扮：`./images/outfit_default.png`
- 战斗装扮：`./images/outfit_battle.png`

---

## 资产索引

> **不要**在这里写复选框列表。当前角色文件夹里实际存在的文件，请看 `MANIFEST.md`（由 skill 在所有文件写完后扫描磁盘生成）。如果你正在阅读这份档案、发现某个引用文件不存在，那就是清单的真相而不是这里的描述——请直接重写缺失的文件。

主要相关文件（参考路径，存在性以 MANIFEST.md 为准）：
- `system_prompt.md` — 角色扮演用的 LLM system prompt
- `dialogue_samples.md` — 扩充的对白样本
- `consistency.yaml` — 一致性参数（生图必读）
- `prompts/` — 各场景生图 prompt

---

*最后更新：{{YYYY-MM-DD}}*
