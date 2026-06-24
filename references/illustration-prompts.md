# 小红书配图 Prompt 模板

小红书配图要求:吸引眼球、信息密度高、竖版为主。

> **配图工作流**:内容分析(`content-analysis.md`)→ 选预设(`presets.md`)→ 选布局(`layouts.md`)→ **查兼容矩阵**(下方)→ 设计 Swipe Flow(`swipe-flow.md`)→ 评估 Hook(`hook-analysis.md`)→ 用下方风格模板生成 prompt

> **⚠️ 安全区**:所有配图必须遵守 `layouts.md` 中的安全区规范。底部 10% 不放关键信息,右上角避开互动按钮区。每个 prompt 末尾追加安全区指令。

---

## 风格 × 布局 兼容矩阵

选定风格和布局后,必须查此矩阵确认组合合理。有 ✗ 的组合会导致风格特征和布局结构冲突,出来效果差。

| 风格 \ 布局 | sparse | balanced | dense | list | comparison | flow | mindmap | quadrant |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 1 手绘涂鸦 | ✓✓ | ✓✓ | ✓✓ | ✓✓ | ✓ | ✓✓ | ✓ | ✓ |
| 2 科技感 | ✓ | ✓✓ | ✓✓ | ✓ | ✓✓ | ✓ | ✓ | ✓✓ |
| 3 Notion极简 | ✓✓ | ✓✓ | ✓ | ✓✓ | ✓ | ✓✓ | ✓✓ | ✓ |
| 4 丝网印刷海报 | ✓✓ | ✓ | ✗ | ✗ | ✓✓ | ✗ | ✗ | ✓ |
| 5 手写笔记 | ✗ | ✓ | ✓✓ | ✓✓ | ✓ | ✓ | ✓ | ✗ |
| 6 手绘信息图 | ✓ | ✓✓ | ✓✓ | ✓ | ✓ | ✓✓ | ✓✓ | ✓ |
| 7 截图+标注 | ✓ | ✓✓ | ✓ | ✓✓ | ✓✓ | ✓✓ | ✗ | ✗ |
| 8 杂志封面 | ✓✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
| 9 拼贴剪报 | ✓✓ | ✓✓ | ✓ | ✗ | ✗ | ✗ | ✗ | ✗ |
| 10 复古插画 | ✓✓ | ✓✓ | ✓ | ✓ | ✗ | ✓ | ✗ | ✗ |
| 11 黑板粉笔 | ✓✓ | ✓ | ✓✓ | ✓✓ | ✗ | ✓ | ✓ | ✗ |

> ✓✓ 强推荐 | ✓ 可用 | ✗ 不推荐
>
> 核心逻辑:
> - 丝网印刷海报靠负空间+大色块,密集布局会破坏其视觉张力
> - 手写笔记风格本身就是密集的,稀疏布局与"学霸笔记"气质冲突
> - 截图+标注适合线性展示,不适合抽象的脑图/象限布局

**兼容检查**:选定风格+布局后查此矩阵。有 ✗ 则换备选风格或布局。预设(presets.md)已确保其风格+布局组合在 ✓ 以上,可安全使用。

## 调用方式

```bash
# idealab Chat API(首选,团队AK,免费无额度压力)
<WORKSPACE>/scripts/generate-image.sh "prompt内容" output.jpg
# 默认模型 gemini-3.1-flash-image-preview,~25s/张
# 竖版 3:4: --ar 3:4
# 竖版 9:16: --ar 9:16
# 方版 1:1: --ar 1:1

# Seedream 5.0 Lite(降级,idealab 不可用时)
<WORKSPACE>/scripts/seedream-generate.sh "prompt内容" output.jpg "1680x2240" 1

# ComfyUI(兜底)
```

---

## 风格一:手绘涂鸦卡片(推荐,适合经验分享、干货总结)

```
# 角色
你是一位擅长手绘涂鸦风的信息可视化设计师,为社交媒体创作吸引眼球的知识卡片。

# 视觉风格规范
## 色彩
- 主色:珊瑚橙(#FF6B6B),搭配暗红(#C44569)、纯白、深灰(#2D3436)
- 背景为淡米色或纯白
- 重点信息用珊瑚橙高亮

## 线条
- 手绘线条,2-4px 均匀粗细
- 造型简洁几何化,纯色填充
- 无纹理、无阴影、无渐变

## 排版
- 大标题醒目居上(核心观点,不超过 8 字)
- 内容分 3-5 个要点,每个要点配一个简笔图标
- 关键词加粗或用色块强调
- 留白充分,不拥挤

## 文字
- 中文无衬线字体
- 遵循帕累托法则,仅提取核心关键词(3-5字)
- 绝不大段文字

## 禁止事项
- 不要渐变或复杂配色
- 不要 3D 效果
- 不要密集文字

# 输出
- 竖版,比例 3:4
- 中文,直接生成不需要解释

# 内容
[在此描述要可视化的内容]
```

### 适用场景
- 干货总结卡片("3个方法让你...")
- 工具推荐卡片
- 对比分析卡片
- 个人经验分享

---

## 风格二:科技感信息卡(适合 AI/产品/技术内容)

```
极简科技风知识卡片。
深色背景(#0F172A),主色电光蓝(#3B82F6),辅助色青绿(#06B6D4)和纯白。
线性图标风格,细线条(1-2px),霓虹发光效果。
标题大字居上,正文内容分区块展示,每个区块有简笔图标。
中文无衬线字体,关键数据用大号字+亮色强调。
竖版,比例 3:4。
高级感、未来感、信息清晰。

内容:[在此描述要可视化的内容]
```

### 适用场景
- AI 工具评测
- 产品功能拆解
- 技术方案对比
- 数据驱动的结论展示

---

## 风格三:Notion 极简线稿(适合知识科普、概念解读)

```
极简黑白手绘线条信息图。
主色:黑色(#1A1A1A),深灰(#4A4A4A)。
背景:纯白(#FFFFFF)或微黄(#FAFAFA)。
强调色:淡蓝(#A8D4F0)、淡黄(#F9E79F)、淡粉(#FADBD8) - 仅用于少量高亮。
线条:单一粗细的手绘线条,略带抖动,像马克笔随手画。
造型:简笔几何图形,圆圈方块,棍状简笔人物。
最大留白,极致干净,信息用短标签承载(3-5字)。
不要彩色渐变、3D效果、复杂装饰。
不要写实照片元素。
竖版,比例 3:4。中文。

内容:[在此描述要可视化的内容]
```

### 适用场景
- 概念解释、知识科普
- SaaS/效率类工具介绍
- 方法论框架
- 专业/理性调性内容

---

## 风格四:丝网印刷海报(适合观点输出、影评书评)

```
丝网印刷/版画风格海报。
2-4 种扁平纯色,绝不用渐变。
主色对从以下选一组:
  橙+青(#E8751A, #0A6E6E) - 电影感
  红+米(#C0392B, #F5E6D0) - 经典
  蓝+金(#1A3A5C, #D4A843) - 高级感
半色调网点纹理(halftone dots)模拟色调变化。
大胆剪影和符号化图形,不画细节,用形状讲故事。
负空间即叙事(figure-ground inversion)。
文字是构图的一部分(不是贴上去的),粗体压缩无衬线或 Art Deco 风。
纸张颗粒质感底纹。
竖版,比例 3:4。中文。

内容:[在此描述要可视化的内容]
```

### 适用场景
- 观点文章封面(强视觉冲击)
- 影评/书评卡片
- 重大声明/重磅观点
- 文化评论

---

## 风格五:手写笔记照片(适合学习笔记、知识整理)

```
俯拍学生笔记风格照片,白色横线纸上密集手写。
主色:蓝色圆珠笔(#1E3A5F) 写正文,黑色墨水(#1A1A1A) 写标题。
强调:红色笔(#CC0000) 圈重点、画下划线、标星号。
高亮:黄色荧光笔(#FFFF00, 50%透明) 标记关键词。
真实的手写笔迹,有粗细变化,字迹密密麻麻但有结构。
页边空白处挤满补充笔记(蓝色小字)。
简单符号:→ ★ ✓ ✗ ! 123。
不要卡通元素、emoji、彩色装饰。
整张图是"学霸笔记"的真实感照片。
竖版,比例 3:4。中文。

内容:[在此描述要可视化的内容]
```

### 适用场景
- 知识框架整理("学霸笔记"感)
- 考试/面试要点速查
- 读书笔记分享
- 知识密集型总结

---

## 风格六:手绘信息图 / Sketch Notes(适合教育、流程图解、知识总结)

```
手绘教育信息图风格,像高质量的演讲视觉摘要。
背景:暖奶油色(#F5F0E8),微纸张纹理。
区块色:马卡龙蓝(#A8D8EA)、薄藤(#D5C6E0)、薄荷(#B5E5CF)、桃子(#F8D5C4) - 用作信息区块的圆角罩块背景。
强调色:珊瑚红(#E8655A),仅少量用于关键词强调。

所有线条带轻微手绘抖动(wobble),不用完美几何形状。
简笔籽状人物(在桌前工作、思考、对话)。
圆角卡片作为信息分区块,每个区块用一个马卡龙色填充,但填色不完全填满边缘(手绘感)。
涂鸦装饰:小星星、下划线、对勾、箭头、灯泡图标、齿轮图标。
波浪形手绘箭头连接各区块,箭头旁可加小字标注。

字体:
- 标题:粗体手绘字,大而醒目
- 区块内关键词加粗
- 次要文字用深灰小字
- 所有文字必须手绘质感,不用电脑字体

禁止:完美几何形状、写实元素、深色或饱和背景、渐变、光泽效果。
竖版,比例 3:4。中文。

内容:[在此描述要可视化的内容]
```

### 适用场景
- 教育/教程类内容(手绘教程、how-to)
- 流程/工作流图解
- 知识总结、概念图
- 技术解释做得亲切易懂
- 演讲/文章的视觉摘要

### macaron 配色的 Prompt 覆盖规则
当预设包含 macaron 配色时(如 `sketch-card`、`sketch-flow`),上述 prompt 已经内置 macaron 颜色。如果要覆盖为 `warm` 配色,只需替换背景/区块色/强调色的十六进制值,保留所有线条/装饰/字体规则。

---

## 风格七:真实截图 + 标注(适合教程、测评)

不使用 AI 生图,而是**真实截图 + 美化 + 标注**。

### 处理流程
1. 实际操作截图
2. 用 `<WORKSPACE>/scripts/beautify-screenshot.sh` 美化
3. 需要标注时,用圆圈/箭头/文字标注重点区域

### 适用场景
- 产品测评(真实界面)
- 操作教程(步骤截图)
- 效果展示(before/after)

---

## 小红书配图策略

> 详细的 Swipe Flow 设计见 `swipe-flow.md`,预设系统见 `presets.md`,布局体系见 `layouts.md`。

### 封面图(最重要)
- 封面决定 80% 的点击率(详见 `swipe-flow.md` 的"封面 80% 法则")
- 封面固定用 `sparse` 布局:大字标题 + 一个视觉焦点
- 标题必须通过 Hook 评估(≥ 4 星,详见 `hook-analysis.md`)

#### 🔴 封面与正文配图分离规则

> **封面图与正文配图必须属于不同的视觉语言家族。**
>
> - 封面用「艺术感/戏剧性」视觉：名画锚点、拼贴、丝网印刷、油画、水墨等
> - 正文内容页用「功能性/信息传达」视觉：手绘涂鸦卡片、科技感信息卡、Notion 线稿等
> - **禁止**：封面与正文配图在 Rendering 维度上相同
> - **检验标准**：信息流中封面“抓眼球”，内容页“传信息”，两者视觉张力明显不同

#### 封面图七维度体系（Art Reference 驱动）

封面图以 **Art Reference（名画/艺术运动锚点）为核心**，搭配七维度微调。

| 维度 | 小红书常用选项 | 默认 |
|------|--------------|------|
| **Type** | `typography`(大字报)、`hero`(视觉冲击)、`minimal`(极简) | typography |
| **Palette** | `warm`(莫兰迪)、`mono`(黑白)、`macaron`(马卡龙)、`kraft`(牛皮纸)、`ink-blue`(蓝墨水)、`pop-candy`(波普糖果)、`forest`(森林) | warm |
| **Rendering** | `hand-drawn`(手绘)、`flat-vector`(扁平)、`screen-print`(丝印)、`magazine`(杂志)、`collage-zine`(拼贴)、`retro-illustration`(复古插画)、`chalkboard`(黑板粉笔) | hand-drawn |
| **Text** | `title-only`、`text-rich`(多要点) | title-only |
| **Mood** | `bold`(信息流抢眼)、`balanced`、`subtle`(克制) | bold |
| **Font** | `casual`(随意手写)、`bold-sans`(粗黑体)、`serif`(衬线)、`display`(装饰体) | bold-sans |
| **Layout** | `top-title`(标题在上)、`center-title`(标题居中)、`split-vertical`(上下分区) | top-title |

**封面预设速查:**

| 预设名 | Type | Palette | Rendering | 适用 |
|--------|------|---------|-----------|------|
| `xhs-knowledge` | typography | warm | hand-drawn | 干货/方法论(**最常用**) |
| `xhs-bold` | typography | mono | screen-print | 观点/爬坑 |
| `xhs-cute` | minimal | macaron | flat-vector | 生活/好物 |
| `xhs-tech` | hero | vivid | flat-vector | AI/产品测评 |
| `xhs-magazine` | typography | ink-blue | magazine | 深度长文/收藏型 |
| `xhs-collage` | typography | kraft | collage-zine | 经验分享/避坑/真实故事 |
| `xhs-retro` | hero | kraft | retro-illustration | 科普/概念解释/教程 |
| `xhs-chalk` | typography | 默认(暗底) | chalkboard | 教程/框架/知识体系 |
| `xhs-pop` | typography | pop-candy | screen-print | 争议观点/颠覆认知 |
| `xhs-zen` | minimal | forest | hand-drawn | 成长感悟/反思/慢节奏 |

#### Art Reference 封面预设库（16 个，小红书版）

Art Reference 是封面图的**核心视觉方向**。小红书信息流竞争激烈，名画元素可以更大胆——占 30-50% 画面。

**核心原则：**
1. **每篇笔记封面必须选一个 Art Reference 预设**（与正文内容页风格强制不同）
2. 名画元素可占 30-50% 画面，但**标题仍然是第一视觉**
3. 缩略图检验：180px 宽缩略图下，标题+风格都可辨认
4. 提取名画的视觉语言（色调、笔触、构图），不是直接复刻名画

##### 经典名画系列（8 个）

| Reference ID | 艺术锚点 | 竖版用法 | 推荐搭配 | 适用场景 |
|---|---|---|---|---|
| `starry-night` | 梵高《星空》漩涡笔触 | 漩涡笔触从底部涌起，标题在上半部留白处 | oil-painting + gallery | 趋势/浪潮/变革 |
| `great-wave` | 葛饰北斋 浪花线条 | 浪花从底部涌起，标题在上半部留白处 | ukiyo-e + edo | 颠覆/冲击/力量 |
| `mondrian` | 蒙德里安 几何色块 | 色块网格分割版面，标题在最大色块内 | flat-vector + pop-candy | 架构/分类/系统 |
| `warhol` | 沃霍尔 波普重复 | 重复图案 2×2/3×3 排列，标题叠加在中央 | screen-print + pop-candy | 争议/大胆/反直觉 |
| `monet-garden` | 莫奈印象派光影 | 印象派色彩铺满背景，下半部暗色带+白字标题 | oil-painting + warm | 洞察/柔性观点/兰思 |
| `song-dynasty` | 宋代山水留白 | 大面积留白，角落水墨意境，标题居中 | ink-wash + forest | 哲理/本质/极简 |
| `bauhaus` | 包豪斯几何原色 | 几何形状堆叠，标题在主色块内 | flat-vector + pop-candy | 方法论/工具/效率 |
| `film-noir` | 黑色电影光影 | 强光影剪影铺满，标题在高亮区域 | digital + darkroom | 故事/深夜/个人叙事 |

##### 现代艺术系列（4 个）

| Reference ID | 艺术锚点 | 竖版用法 | 推荐搭配 | 适用场景 |
|---|---|---|---|---|
| `klimt-gold` | 克里姆特金箔装饰 | 金箔纹样铺满背景，深色块承载标题 | oil-painting + gallery | 里程碑/高价值/成就 |
| `matisse-cut` | 马蒂斯剪纸色块 | 有机曲线色块作为标题背景/装饰 | collage-zine + macaron | 创意/简约/大胆表达 |
| `rothko-field` | 罗斯科色域渗透 | 2-3层水平色块铺满，标题浮于色块交界处 | painterly + warm | 情感/深层思考/内省 |
| `kandinsky` | 康定斯基抽象几何 | 抽象几何+线条分布，标题在留白处 | flat-vector + pop-candy | 多元素/协作/抽象概念 |

##### 风格流派系列（4 个）

| Reference ID | 艺术锚点 | 竖版用法 | 推荐搭配 | 适用场景 |
|---|---|---|---|---|
| `art-deco` | 装饰艺术对称金线 | 对称装饰框+金线勾边，标题居中 | digital + ink-blue | 优雅/规则/高端质感 |
| `cyberpunk` | 赛博朋克霆虹电路 | 暗底+霆虹发光文字，背景电路纹理 | digital + neon | AI/未来/技术极客 |
| `picasso-cubism` | 毕加索多角度片段 | 主题拆解为几何片段，标题嵌入片段间 | collage-zine + pop-candy | 多角度/解构/复杂问题 |
| `escher-loop` | 埃舍尔不可能图形 | 循环/阶梯结构居中，标题在结构上方 | flat-vector + ink-blue | 递归/悖论/系统循环 |

**构图约束(封面图 prompt 末尾必附):**
```
Composition rules for Xiaohongshu cover (vertical 3:4, 1680×2240):
- Title text occupies 40%+ area, must be immediately readable at 180px thumbnail width
- Title placement: upper 40-60% of image (eye scans top-down in feed)
- Single visual focal point below title, generous whitespace (40-60%)
- NO realistic human faces, use simplified silhouettes or icons
- Bold high-contrast colors for feed competition
- Chinese text large, clear, no overlap with busy visual areas
- Bottom 10% clear (app UI safe zone, ~224px)
- Right-top corner 120×120px clear (interaction buttons ❤ 📌)
- Background fills entire canvas to all four edges, NO outer border, NO frame, NO floating card (use poster/海报, never "card")
- All title/detail text within 8% padding from edges, never cut off at boundary
- If using Art Reference: element can occupy 30-50% but must NOT compete with title
- Vertical flow only: all information stacks top-to-bottom, never side-by-side
```

#### 封面安全区示意图

```
┌──────────────────────────┐
│  ←── 右上角留空 ──→  ❤ 📌 │  ← 互动按钮区
│                          │
│   ┌──────────────────┐   │
│   │                  │   │
│   │    主标题区域     │   │  ← 上半部 40-60%
│   │  (占40%+面积)    │   │     标题必须在这里
│   │                  │   │
│   └──────────────────┘   │
│                          │
│   ┌──────────────────┐   │
│   │  视觉焦点/Art Ref │   │  ← 中下部
│   │  (单一元素)       │   │
│   └──────────────────┘   │
│                          │
│▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒│  ← 底部10% 安全区
└──────────────────────────┘
     3:4 竖版 (1680×2240)
```

### 正文配图
- 图文笔记建议 4-6 张图
- 第 1 张 = 封面(`sparse`,吸引点击)
- 第 2 张 = 铺垫(`balanced`,建立背景/共鸣)
- 第 3-N 张 = 核心内容(跟随预设默认布局)
- 最后 1 张 = 结尾(`sparse`,CTA + 互动引导)
- 每张图底部加 Swipe Hook(除最后一张)

### 使用决策(已升级为预设系统)
```
内容类型判断 → 自动推荐预设(见 presets.md):
├─ 干货分享 / 方法论 → knowledge-card(手绘涂鸦 + dense)
├─ 排行 / 清单 / 避坑 → checklist(手绘涂鸦 + list)
├─ 教程 / 流程 / 步骤 → step-guide(手绘涂鸦 + flow)
├─ AI/产品/技术分析 → tech-insight(科技感 + balanced)
├─ 产品对比 / 方案PK → vs-compare(科技感 + comparison)
├─ 个人经历 / 故事 → pm-story(手绘涂鸦 + balanced)
├─ 封面 / 金句 → cover-hook(sparse)
└─ 教程/测评/实操 → 风格三(真实截图)
```

### 三策略分化(多方案选择)

每次配图不止出 1 个方案,出 **2 个差异化方案**供老板选择:

```markdown
## 方案 A(信息密集型)
- 预设:knowledge-card
- 张数:5-6 张
- 特点:高密度知识卡,每张 5+ 信息点,适合收藏

## 方案 B(叙事驱动型)
- 预设:pm-story
- 张数:4-5 张
- 特点:个人视角带入,每张 2-3 个点 + 场景感,适合共鸣

[老板指定时可出方案 C]
## 方案 C(极简海报型)
- 预设:cover-hook 全系列
- 张数:3-4 张
- 特点:大字报风,每张只 1 个核心观点,最强视觉冲击
```

方案 A 和 B 必须在**风格、布局、张数、信息密度**上有明显差异。

## 生图工具优先级

**idealab Chat API → Seedream 5.0 Lite → ComfyUI**

### 1. idealab Chat API（首选）
- 脚本: `<WORKSPACE>/scripts/generate-image.sh "prompt" output.jpg`
- 团队 AK，免费无额度压力，~25s/张
- 默认模型: `gemini-3.1-flash-image-preview`
- 可选: `gemini-2.5-flash-image`（更快 ~10s）、`gemini-3-pro-image-preview`（最高质量）
- ℹ️ 生成后自动去水印

### 2. Seedream 5.0 Lite（降级）
- 脚本: `<WORKSPACE>/scripts/seedream-generate.sh "prompt" output.jpg "size" n`
- 0.22 元/张，idealab 不可用时才用
- 竖版尺寸: `1440x2560`(9:16) 或 `1680x2240`(3:4)
- 方版尺寸: `1920x1920`(1:1)
- ⚠️ 最小像素要求 ≥ 3686400

### 3. ComfyUI（兜底）
- 本地运行，完全免费，但速度慢

## 生图注意事项

- 小红书竖版为主(3:4 或 9:16)
- 同一篇笔记的多张配图保持风格统一
- Seedream 无水印,nano-banana-pro 需去水印
- 中文文字必须清晰可读,不清晰则重新生成
- 所有配图 prompt 末尾追加安全区指令(见 `layouts.md`)
- ⛔ **Prompt 先存后生**:每张图的 prompt 先保存到文件(笔记目录下 `prompts/NN-{position}-{slug}.md`),再调用 Seedream 生成。失败时改文件重试不用重新构思,全部 prompt 有存档可回溯

## 多图系列视觉一致性

### 文本锚点(默认方式)

生成第一张图后,记录成功图的关键特征。后续图片 prompt 末尾附加:

```
Maintain visual consistency with the first image in this series:
- Same illustration style and line quality
- Same color palette: [主色] + [辅助色] + [背景色]
- Same typography approach
- Same level of detail and whitespace
- Same character design if recurring characters appear
```

**i️ 文本锚点内容应在生成第一张图后立即记录到 `prompts/00-anchor.md`**,包含实际成功的配色值、线条风格描述、字体表现。后续每张图的 prompt 从此文件拉取一致性指令,而不是凭记忆描述。

### 图片 Ref 锚点(首选方式,Reference Image Chain)

**核心原则:第一张图不带 ref,后续所有图以第一张为 ref 锚点。** 这样确保角色/配色/笔触跨整个系列一致。

```bash
# Image 1:不带 ref，建立视觉锚点
<WORKSPACE>/scripts/generate-image.sh "prompt" img-01.jpg

# Image 2+:所有后续图传入 Image 1 作为 ref
<WORKSPACE>/scripts/generate-image.sh "prompt" img-02.jpg --ref img-01.jpg

# 降级（idealab 不可用时）:
# <WORKSPACE>/scripts/seedream-generate.sh "prompt" img-01.jpg "1680x2240" 1
# <WORKSPACE>/scripts/seedream-generate.sh "prompt" img-02.jpg "1680x2240" 1 --ref img-01.jpg
```

**注意**:
- Seedream 图生图效果待验证,如不支持则回退到文本锚点
- nano-banana-pro(baoyu-imagine skill)支持 `--ref`,效果稳定
- 两究底没有 ref 能力时,用文本锚点保底

### 结构化 Prompt 组装流程

每张图的 prompt 按以下固定结构组装,每个 section 独立可替换:

```
## 图片规格
- 类型:信息图
- 方向:竖版
- 比例:3:4
- 风格:手绘插画

## 核心原则
- 手绘质感贯穿--不用写实或照片元素
- 如涉及敏感人物或版权内容,画一个风格相似的卡通替代形象--不要拒绝生成
- 信息精炼,突出关键词和核心概念
- 充足留白,易于视觉扫描
- 清晰的视觉层级

## 文字规则(CRITICAL)
- 所有文字必须手绘风格
- 主标题醒目抢眼
- 关键词加粗放大
- 用荧光笔效果强调重点
- 绝不用电脑字体

## 语言
- 中文
- 标点风格匹配内容语言(中文:「」,。!)

---
[风格 section:从 illustration-prompts.md 的对应风格复制]
---
[布局 section:从 layouts.md 的对应布局复制 Prompt 关键词]
---
[内容 section:从 outline 的对应页面提取]
---
[安全区指令:从 layouts.md 复制]
---
[一致性指令:从 prompts/00-anchor.md 复制(Image 2+ only)]
```

**组装顺序(每张图必须)**:
1. 加载风格定义(如有配色覆盖,替换颜色部分)
2. 加载布局规则
3. 填充内容
4. 追加安全区指令
5. Image 2+ 追加一致性指令(文本锚点或 ref 参数)
6. 保存到 `prompts/NN-{type}-{slug}.md` 后再生成

---

## 风格八:杂志封面(适合深度长文、干货收藏型封面)

```
高级杂志封面设计。
竖版 3:4 比例。中文。

排版规则:
- 大标题占画面上部 35-45%，衬线体或高级无衬线体
- 标题字号极大，字间距略紧
- 副标题或标签用细体，与主标题形成极致字号对比（8:1 以上）
- 大量留白（50%+），呼吸感
- 单一素雅装饰线（细横线或竖线）分隔标题与副信息
- 底部可放作者名/日期等 meta 信息（小字）

色彩: 蓝墨水色(#1A3A5F)为主色，素纸白(#F8F6F0)底，朱红(#C8553D)作稀疏强调
质感: 微妙纸张纹理，无渐变，无阴影，无3D效果
参考调性: Monocle 杂志 / KINFOLK / 物外设计

内容:[在此描述封面主题]
```

### 适用场景
- 深度分析文章封面
- “值得收藏”型干货
- 系列文章统一风格
- 展现专业度和品味

---

## 风格九:拼贴剪报(适合经验分享、避坑、真实故事封面)

```
手工拼贴剪报风格封面。
竖版 3:4 比例。中文。

视觉元素:
- 多层叠加：便签纸、彩色胶带（washi tape）、撕边纸片、贴纸
- 标题写在便签纸或胶带上，手写体或打字机体
- 背景是牛皮纸或笔记本纸纹理
- 装饰：回形针、图钉、手绘箭头、圆圈标注、星星贴纸
- 错位排列，不对齐，有“手工制作”的随意感
- 可嵌入一两个简笔画小图标

色彩: 牛皮纸底(#D4A574)，彩色胶带(淡蓝#A8D8EA、淡黄#F8E9B0、淡粉#F8D5C4)
强调: 复古红(#C0392B)用于关键词高亮
质感: 纸张纹理、胶带半透明叠加、轻微阴影（贴纸翘起感）

内容:[在此描述封面主题]
```

### 适用场景
- “我踩过的坑”经验分享
- 避坑指南
- 个人真实故事
- 生活感/DIY感/亲和力强的内容

---

## 风格十:复古插画(适合科普、概念解释、教程封面)

```
60-70年代复古教科书插画风格封面。
竖版 3:4 比例。中文。

视觉特征:
- 圆润线条、温暖色调、略带颗粒感
- 人物/物体用简化几何形态，不追求写实
- 大色块平涂，有限配色(3-4色)
- 标题用粗体圆角无衬线字体，复古但清晰
- 可用箭头、数字标注、虚线框做解释性标注
- 整体感觉“怀旧但不过时”，像一本好看的老教材

色彩: 牛皮纸底(#D4A574)，暖棕(#8B5E3C)勾线，奶油黄(#F5E6D0)填充
强调: 深蓝(#1A5276)或复古红(#C0392B)做标题和关键信息
质感: 轻微纸张颗粒，印刷半色调网点，无光泽效果

内容:[在此描述封面主题]
```

### 适用场景
- “一张图看懂XXX”科普
- 概念入门解释
- 教程/操作指南封面
- 想传达“易懂”、“友好”、“有趣学习”的调性

---

## 风格十一:黑板粉笔(适合教程、知识体系、框架型封面)

```
深色黑板 + 粉笔手写风格封面。
竖版 3:4 比例。中文。

视觉特征:
- 深绿/深灰黑板背景(#2D3436 或 #1B4332)
- 白色粉笔(#F5F5F5)写标题，笔触有粗细变化
- 彩色粉笔做强调：黄色(#FBBF24)、天蓝(#60A5FA)、粉色(#F472B6)
- 可画简单框图、箭头、下划线、圆圈标注
- 标题大而粗，有“老师板书”的随意感
- 底部可有粉笔灰/擦除痕迹增加真实感

色彩: 深色板底，白色为主文字，彩色粉笔做标注和强调（不超过3种彩色）
质感: 粉笔粗糙笔触、板面微弱反光、粉尘颗粒
参考调性: 学校黑板报 / 咖啡馆菜单黑板 / TED 演讲白板

内容:[在此描述封面主题]
```

### 适用场景
- 教程/教学类
- 知识框架/体系梳理
- “全景图”/“知识地图”类内容
- 传达“老师教你”、“课堂感”的调性
