# ecom-gpt-image

一个通用的 AI 电商图片生成 Skill，适用于 Claude Code、Codex 和其他 AI Agent。

基于用户提供的产品图片 + 文字描述，直接调用 OpenAI 兼容图像生成 API（如 GPT-Image-2），生成高质量电商视觉素材。

## 核心能力

- **参考图生图**：贴上产品图，自动生成商品主图、详情页、广告图、社媒图
- **25 种场景模板**：白底图、场景图、平铺图、海报、UGC、直播间、杂志风等
- **Campaign Style Lock**：整套图片风格一致性保证
- **转化驱动**：内置视觉驱动、痛点驱动、情感驱动三种电商转化策略
- **整套图片包**：一键生成 5 张主图 + 7-9 张详情页图片

## 安装

### Claude Code

```bash
# 方式 1: 通过 /install 命令
/install https://github.com/<your-username>/ecom-gpt-image

# 方式 2: 手动克隆
git clone https://github.com/<your-username>/ecom-gpt-image.git ~/.claude/skills/ecom-gpt-image
```

### 手动安装

克隆到任意位置，在你的 AI agent 配置中引用 `SKILL.md` 文件路径。

## 配置

### 1. 创建 .env 文件

```bash
# 全局配置（推荐，所有项目通用）
mkdir -p ~/.config/ecom-gpt-image
cp .env.example ~/.config/ecom-gpt-image/.env
# 编辑填入你的 API key
```

或在项目目录下创建 `.env`：

```bash
cp .env.example .env
# 编辑填入你的 API key
```

### 2. 必填变量

| 变量 | 说明 | 示例 |
|---|---|---|
| `IMG_BASE_URL` | API 根地址 | `https://api.apimart.ai/v1` |
| `IMG_MODEL` | 图片模型名 | `gpt-image-2` |
| `IMG_API_KEY` | API key | `sk-xxx` |

### 3. 可选变量

| 变量 | 说明 | 默认值 |
|---|---|---|
| `IMG_OUTPUT_DIR` | 图片保存目录 | `generated-images/` |

## 使用

在 Claude Code / Codex 对话中直接使用：

```
# 贴上产品图片后说：
帮我生成一套电商主图，白底 + 场景图

# 只要 Prompt，不直接生图：
给这个产品写一套 Amazon A+ 详情页的图片 Prompt

# 指定风格：
用奢华风格生成这个手表的商品主图
```

### 命令行直接调用

```bash
# 基础生图
python3 scripts/generate_image.py --prompt "clean product hero image..." --size 1:1

# 基于参考图
python3 scripts/generate_image.py --prompt "..." --image product.jpg --size 1:1 --resolution 2k

# 从文件读取 prompt
python3 scripts/generate_image.py --prompt-file prompt.txt --output-dir ./outputs
```

## 场景模板

内置 25 种电商视觉场景模板，覆盖：

| 编号 | 场景 | 编号 | 场景 |
|---|---|---|---|
| 01 | 白底主图 | 14 | 套装组合 |
| 02 | 场景生活图 | 15 | 直播间 |
| 03 | 平铺图 | 16 | 虚拟试穿 |
| 04 | 细节微距 | 17 | 拆解爆炸图 |
| 05 | 海报 Banner | 18 | 隐形模特 |
| 06 | 社交媒体 | 19 | 多角度网格 |
| 07 | UGC 买家秀 | 20 | 杂志编辑 |
| 08 | 模特展示 | 21 | 季节活动 |
| 09 | 前后对比 | 22 | 奢华氛围 |
| 10 | 包装礼盒 | 23 | 设备模型 |
| 11 | 信息图 A+ | 24 | 店铺门面 |
| 12 | 创意概念 | 25 | 运动健身 |
| 13 | 尺寸规格 | | |

## 项目结构

```
ecom-gpt-image/
├── SKILL.md                    # Skill 定义（AI Agent 读取）
├── README.md                   # 本文件
├── .env.example                # 配置模板
├── .gitignore
├── scripts/
│   └── generate_image.py       # 生图脚本
└── references/
    └── templates/              # 25 个场景模板
        ├── 01-hero-image.json
        ├── 02-lifestyle-scene.json
        └── ...
```

## 安全说明

- `.env` 文件包含 API key，已在 `.gitignore` 中排除
- Skill 不会在输出中暴露、回显或提交 API key
- 建议使用 `~/.config/ecom-gpt-image/.env` 全局配置，避免在项目中泄露

## License

MIT
