# Poster 海报生成项目

一个由 AI 设计智能体（TRAE SOLO CN）生成的可视化海报集合。项目包含两类作品：

1. **文件夹式静态设计海报**（12 个）：每个文件夹是一个独立、自包含的 AI 生成海报工程，带有完整的设计元数据、品牌设计变量与产物 HTML。
2. **单文件 3D 太空海报**（4 个，位于 `3d-posters/`）：基于 Three.js / WebGL 的交互式 3D 场景，可直接在浏览器打开。

> 来源线索：`orchestration-summary.json` 中记录的导出路径为
> `C:\Users\admin\AppData\Roaming\TRAE SOLO CN\ModularData\ai-agent\work-mode-projects\...`，
> 表明这些海报由 TRAE SOLO 的「work-mode / 设计智能体」自动编排生成。

---

## 目录结构

```
poster/
├── README.md                       # 本文件
├── package.json                    # Node 工程（仅依赖 puppeteer）
├── package-lock.json
├── node_modules/                   # puppeteer 依赖（建议加入 .gitignore）
│
├── # —— 单文件 3D 海报（Three.js / WebGL，归入 3d-posters/）——
├── 3d-posters/                     # 3D 太空海报集合
│   ├── black-hole-3d.html          # 黑洞吸积盘 3D 场景
│   ├── ocean-world.html            # 海洋世界 3D 场景
│   ├── solar-system-poster.html    # 太阳系 3D 场景
│   └── trinary-star-system.html    # 三合星系统 3D 场景
│
├── # —— 文件夹式静态海报（每个目录结构相同）——
├── ancient-egypt-poster/          # 古埃及展览海报
├── ancient-greece-poster/          # 古希腊展览海报
├── chinese-style-poster/           # 中国风海报
├── japanese-style-poster/          # 日式风格海报
├── mayan-culture-poster/           # 玛雅文化海报
├── monet-exhibition-poster/        # 莫奈印象派展览海报
├── picasso-style-poster/           # 毕加索风格海报
├── happy-birthday-poster/          # 生日快乐海报
├── birthday-multi-style/           # 多风格生日合集（5 页 / 16 图）
├── birthday-slideshow/             # 生日海报轮播
├── earth-from-space-wallpaper/     # 太空地球壁纸（5 页 / 7 图）
└── poster-collection-video/        # 海报集合（视频向）
```

---

## 单个海报文件夹的构成（标准骨架）

每个 `*poster/`、`*style/`、`*wallpaper/` 文件夹都遵循同一套结构：

| 文件 / 目录 | 作用 |
|---|---|
| `<name>.design` | **画布设计元数据**（JSON）。记录节点（page / image）及其在画布上的坐标、标题、以及 `devMetadata`（如 `htmlSrc: "pages/poster.html"`、`imageSrc: "assets/xxx.jpg"`）。 |
| `generation-tree.json` | **页面生成树**。描述「page-leaf」节点到产物 HTML 的映射（如 `output: "pages/poster.html"`），含共享/私有区域、可变插槽等编排信息。 |
| `orchestration-summary.json` | **完整编排摘要**（仅部分文件夹有）。包含：风格简报（styleDefinitionBrief）、设计判读（designRead）、风格连续性锚点（色彩/形状/字体/间距/组件/表面/图像/交互）、设计约束（radiusMax、间距基、字号）、品牌 token 命名引用（带前缀，如 `--ae-primary`）、产品上下文（kitType: poster、productType）与页面/资产清单。 |
| `colors_and_type.css` | **设计变量源文件**。以品牌前缀定义 CSS 自定义属性（色彩系统、字体系统、字号阶梯、字重、行高、字距、形状、间距），并附带少量排版工具类（如 `.ae-title`、`.ae-text-hero`）。 |
| `pages/` | **生成的产物 HTML**。设计 token 已内联进 `<style id="theme-vars">` 块，图片通过相对路径 `./assets/...` 引用，单文件即可浏览。 |
| `partials/` | 可复用 HTML 片段（本项目中大多为空，仅作结构占位）。 |
| `assets/` | 海报使用的图片资源（`.jpg` 主视觉等）。 |
| `.uploads/`（部分为隐藏缓存） | 智能体内部上传缓存，非交付物。 |

**关键约定**
- 每个海报使用独立的 **品牌前缀**（如古埃及为 `ae`：`--ae-primary`、`--ae-background`…），互不污染。
- `deviceType` 取值：`freeSize`（自由画幅，多为单页海报）或 `desktop`（含多页 / 多图的合集类）。
- 产物 HTML 自包含（内联 CSS + 相对图片），可直接用浏览器打开；字体多来自 Google Fonts（Cinzel、Noto Serif SC 等），需联网加载。

---

## 作品清单

### 文件夹式静态海报（12 个）

| 文件夹 | 项目名 | 设备 | 页数 | 图片数 | 含编排摘要 |
|---|---|---|---:|---:|:---:|
| ancient-egypt-poster | 古埃及海报 | freeSize | 1 | 1 | ✅ |
| ancient-greece-poster | 古希腊展览海报 | desktop | 2 | 1 | ✅ |
| chinese-style-poster | 中国风海报 | freeSize | 1 | 1 | ✅ |
| japanese-style-poster | 日式风格海报 | freeSize | 1 | 1 | ✅ |
| mayan-culture-poster | 玛雅文化海报 | freeSize | 1 | 1 | ✅ |
| monet-exhibition-poster | 莫奈印象派展览海报 | freeSize | 1 | 1 | ✅ |
| picasso-style-poster | 毕加索风格海报 | freeSize | 1 | 1 | ✅ |
| happy-birthday-poster | 生日快乐海报 | freeSize | 1 | 1 | — |
| birthday-multi-style | 多风格生日快乐动态海报 | desktop | 5 | 16 | — |
| birthday-slideshow | 生日海报轮播 | freeSize | 1 | 8 | — |
| earth-from-space-wallpaper | 太空地球壁纸 | desktop | 5 | 7 | — |
| poster-collection-video | 海报集合体 | desktop | 1 | 7 | — |

### 单文件 3D 海报（4 个，根目录）

| 文件 | 主题 | 技术 |
|---|---|---|
| black-hole-3d.html | 黑洞吸积盘 | Three.js (CDN) + WebGL + OrbitControls |
| ocean-world.html | 海洋世界 | Three.js (CDN) + WebGL |
| solar-system-poster.html | 太阳系 | Three.js (CDN) + WebGL |
| trinary-star-system.html | 三合星系统 | Three.js (CDN) + WebGL + OrbitControls |

---

## 技术栈

- **静态海报**：原生 HTML + CSS（内联设计 token），Google Fonts 网络字体。无构建步骤，产物即为最终页。
- **3D 海报**：Three.js（通过 CDN 引入），WebGL 渲染，含 OrbitControls 轨道交互。
- **工程依赖（已清理）**：`package.json` 曾声明 `puppeteer ^25.3.0`，但全项目无任何代码 `import`/`require` 它，也无构建脚本或 `index.js`。经确认其为生成阶段的工具残留，**`node_modules/` 已物理删除（约 22.8 MB）**，交付物不需要任何 Node 运行时。若需恢复可执行 `npm install`。
- **生成方式**：由 AI 设计智能体（TRAE SOLO CN）基于风格简报自动编排，输出 `.design` / `generation-tree.json` / `orchestration-summary.json` 元数据与 `pages/*.html` 产物。

---

## 如何预览

**静态海报（文件夹式）**
```bash
# 直接打开产物页
open ancient-egypt-poster/pages/poster.html
# 或起一个本地静态服务器（推荐，避免部分浏览器对相对路径的限制）
python3 -m http.server 8080
# 然后访问 http://localhost:8080/<folder>/pages/<page>.html
```

**3D 海报（位于 `3d-posters/`）**
```bash
# 直接用浏览器打开对应 .html；需联网加载 Three.js CDN 与字体
open 3d-posters/black-hole-3d.html
```

---

## 备注与待清理项

- **`--css-relative-path`（根目录，约 104 KB）**：经检查为**损坏/误导出的拼接文件**——内容由多个 `<!DOCTYPE html>` 文档首尾相接拼成（内含一个 `light` 主题页与一个「毕加索生日快乐」页）。疑似导出工具异常产生的临时产物，**已删除**。
- **`node_modules/`**、**`.uploads/`**、**`.workbuddy/`**：分别为 npm 依赖、智能体上传缓存、本地工作记忆，**已加入 `.gitignore`**，不纳入版本管理。
- **`partials/`** 9 个空占位目录**已删除**；其余文件夹的 `partials/` 本就不存在或为结构占位。
- 部分文件夹（如 `birthday-*`、`earth-from-space-wallpaper`、`poster-collection-video`）**缺少 `orchestration-summary.json`**，风格信息仅存于 `.design` 与 `colors_and_type.css`，如需复用其设计语言可据此重建摘要。

---

## 一句话总结

这是一个 AI 设计智能体产出的「海报作品集」：12 套带完整设计元数据与品牌变量的文化/生日主题静态海报，外加 4 个交互式 Three.js 3D 太空场景，全部为可直接浏览器打开的自包含 HTML。
