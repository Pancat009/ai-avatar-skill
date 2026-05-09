# 各模型生图 Prompt 模板

不同 AI 生图模型的 prompt 写法差异巨大。同一段中文描述喂给即梦和 Midjourney 效果会差很多。这份文档给出每个主流模型的写法和模板。

---

## 通用结构（所有模型都需要）

```
[STYLE]      画风锚点：写实 / 二次元 / 油画 / 水彩 …
[SUBJECT]    主体描述：性别 + 种族 + 年龄 + 关键外貌
[DETAIL]     细节：发型 + 眼睛 + 服装 + 标志特征
[POSE]       姿势 / 表情 / 动作
[SCENE]      背景 / 氛围 / 光照
[QUALITY]    质量词：masterpiece, best quality, detailed
[NEGATIVE]   负面词：low quality, deformed, watermark, …
```

---

## 即梦（JiMeng / Doubao Vision）

特点：中文友好，写自然语言中文即可。质量词用中文也认。

**模板**：

```
[画风], [角色描述], [细节], [姿势], [场景], 高质量, 精致细节, 4K
负面: 低质量, 变形, 水印, 多余手指
```

**三视图**：

```
[画风], [角色描述], 三视图（正面/侧面/背面），角色设定图，
干净浅灰色背景, 中性表情, 无姿势变化, 标准设计图样式,
高质量, 精致细节
```

**Tips**：
- 即梦对中文成语和文化意象响应好（"江南烟雨""赛博朋克霓虹"）
- 颜色用中文 + hex 都可以："墨蓝色 (#0A1628) 的长袍"
- 角色名用引号包起来防止误解释

---

## Midjourney (v6+)

特点：自然语言堆叠，逗号分隔。**支持参数后缀**（--ar --s --v --niji）。

**模板**：

```
<style>, <subject>, <details>, <pose>, <lighting>, <mood>, --ar 3:4 --s 250 --v 6
```

**三视图**：

```
character design sheet, three view (front, side, back),
[character description], turntable, t-pose, neutral expression,
clean white background, model sheet, --ar 16:9 --s 100 --v 6
```

**风格强化**：

- 二次元 → 加 `--niji 6` 或 `anime style, by Makoto Shinkai`
- 写实 → 加 `photorealistic, shot on Canon EOS R5, 85mm`
- 油画 → 加 `oil painting, brushstrokes visible, classical art`

**Tips**：
- Midjourney 不需要质量词（自带高质量）
- 负面词用 `--no` 参数（`--no extra fingers, watermark`）
- `--cref <url>` 可以传角色参考图保持一致性（v6 关键功能）
- `--sref <url>` 可以传画风参考

---

## Stable Diffusion / SDXL / Pony

特点：tag 式，逗号分隔，**支持权重括号**（`(red hair:1.3)`）。

**模板**：

```
masterpiece, best quality, detailed, 
[style tags], 1girl/1boy, [physical tags], [clothing tags], 
[pose], [expression], [background],
[(emphasis:1.2)]
```

**三视图**：

```
masterpiece, best quality, character sheet, multiple views,
front view, side view, back view, turnaround,
1girl, [detailed character description],
neutral expression, t-pose, simple background, white background,
(reference sheet:1.3)
```

**负面 prompt（必填）**：

```
(worst quality:1.4), (low quality:1.4), lowres, blurry,
bad anatomy, bad hands, extra fingers, missing fingers,
watermark, signature, username, text,
deformed, ugly, distorted, mutated
```

**Tips**：
- Pony / NovelAI 模型对二次元 tag 响应最好
- SDXL realistic 用自然描述比 tag 堆叠更好
- 用 LoRA 锁定角色一致性（如训练过角色模型）
- 锁定 seed + 改 prompt 可保持脸部一致

---

## Flux (dev / schnell)

特点：长句自然语言，不需要堆 tag。质量天花板高，但显卡门槛高。

**模板**：

```
A [style] portrait of [character description in flowing prose].
[Pose and expression]. [Background and lighting].
[Specific details about clothing and accessories].
[Mood and atmosphere].
```

**三视图**：

```
A character design reference sheet showing three views (front, side, back) 
of [character description]. Clean white background, neutral expression, 
t-pose, professional concept art style, high detail.
```

**Tips**：
- Flux 对长描述（150+ 词）响应最好，短 prompt 反而效果差
- 不太需要负面 prompt
- 对手部、文字渲染特别好

---

## NovelAI v3 / v4

特点：日系二次元最强，标准 Danbooru tag 格式。

**模板**：

```
[quality tags], [character], [series if applicable],
[physical features], [clothing], [pose], [expression],
[background], [composition tags]
```

**质量 tag 标准组**：

```
masterpiece, best quality, amazing quality, very aesthetic,
absurdres, year 2024
```

**Tips**：
- Tag 顺序就是优先级
- 用 `{tag}` 加权（NovelAI 风格），不是 `(tag:1.1)` 
- 训练数据来自 Danbooru，所以用标准动漫 tag

---

## 跨模型一致性策略

如果用户在不同模型间切换，保持同一个角色像同一个人是难题。建议：

1. **锁定第一次成功的 seed 和 prompt 文本**，存到 `consistency.yaml`
2. **同一会话内只用同一个模型**（不要混着切）
3. **训练 LoRA / 用 reference image**（Midjourney 的 cref，SD 的 ControlNet/IP-Adapter）
4. **手动后期对齐**：第一张图作为"圣经"，后续图都和它做面部相似度对比

---

## Negative Prompt 通用底线

不管什么模型，下面这组负面词总是要包括：

```
low quality, blurry, deformed, ugly, bad anatomy, 
extra limbs, extra fingers, missing fingers, fused fingers,
watermark, signature, text, jpeg artifacts, 
multiple characters (除非确实要多人), 
worst quality, normal quality
```

如果是写实风，加：`anime, cartoon, illustration, drawing, painting`
如果是二次元，加：`photorealistic, 3d render, photograph`
