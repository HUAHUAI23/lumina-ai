# AI Camera Director Skill

**AI 运镜导演技能** - 将场景描述和图片转化为专业视频生成提示词

---

## 🎯 这是什么？

这是一个 Claude Code Skill，帮助你生成专业的 AI 视频提示词。

**核心能力：**
- 📹 **单镜头提示词** - 为单个视频片段生成运镜提示词
- 🎬 **分镜脚本** - 根据多张图生成完整分镜（含转场、时长）
- 🔲 **九宫格支持** - 自动识别并处理九宫格分镜图
- 🌐 **动态学习** - 主动搜索最新的 Sora/Runway/Pika 指南

---

## � 安装教程

### 方式 1: 直接复制（推荐）

1. **下载整个 `camera-director` 文件夹**

2. **放置到你项目的 `.claude/skills/` 目录下**
   ```bash
   your-project/
   └── .claude/
       └── skills/
           └── camera-director/    # ← 放在这里
               ├── SKILL.md
               ├── README.md
               ├── resources/
               └── workflows/
   ```

3. **确认目录结构正确**
   ```bash
   ls -la .claude/skills/camera-director/
   # 应该看到 SKILL.md, README.md, resources/, workflows/
   ```

4. **完成！** Claude Code 会自动发现并使用此 Skill

### 方式 2: Git Clone（如果是独立仓库）

```bash
# 进入你的项目目录
cd your-project

# 创建 skills 目录（如果不存在）
mkdir -p .claude/skills

# 克隆 skill
git clone <skill-repo-url> .claude/skills/camera-director
```

### 方式 3: 手动创建

如果你想从零开始：

```bash
# 创建目录结构
mkdir -p .claude/skills/camera-director/{resources,workflows}

# 复制核心文件
# - SKILL.md (主入口，必需)
# - resources/*.md (知识库文件)
# - workflows/*.md (工作流文件)
```

---

## ✅ 验证安装

安装后，在 Claude Code 中输入以下测试：

```
帮我生成一段视频提示词：赛博朋克街道，主角在雨中奔跑
```

如果 Claude 返回包含 `Camera Movement:` 和 `Subject & Action:` 的 4 段式提示词，说明安装成功！

---

## �📁 目录结构

```
.claude/skills/camera-director/
├── SKILL.md                    # 主入口
├── resources/
│   ├── knowledge-base.md       # 运镜知识库
│   ├── platform-prompts.md     # Sora/Runway/Pika 指南
│   ├── transitions.md          # 转场类型参考
│   ├── storyboard-guide.md     # 分镜技术指南
│   └── validation-rules.md     # 验证规则
└── workflows/
    ├── single-shot-workflow.md # 单镜头工作流
    └── storyboard-workflow.md  # 分镜脚本工作流
```

---

## 🚀 如何使用

### 方式 1: 自动激活

当你的描述中包含以下关键词时，Claude 会自动使用此 Skill：

```
video prompt, camera movement, 运镜, 分镜, storyboard, Sora, Runway, Pika
```

### 方式 2: 直接请求

**单镜头示例：**
```
这张图，帮我生成一段视频提示词，缓慢推进到人物面部，她说"我们走吧"
```

**分镜脚本示例：**
```
这9张图是一个告别故事的分镜，帮我生成完整的分镜脚本
```

**九宫格示例：**
```
[上传一张九宫格图]
这是我的分镜草稿，帮我生成脚本
```

---

## 📤 输出示例

### 单镜头输出

```
Cyberpunk thriller, tracking shot, neon-lit rainy street.

Camera Movement: Camera rapidly tracks alongside Image 1 as they sprint.

Subject & Action: Image 1 runs desperately, shouting "快跑!" in panic.

Environment & Mood: Wet pavement reflects neon signs. Heavy rain.
```

### 分镜脚本输出

```markdown
# 告别 分镜脚本
**总时长:** 18秒 | **镜头数:** 4 | **风格:** 文艺

---
## 镜头 1 | 4秒 | 远景
**转场:** 淡入 | **运镜:** Slow Crane Down
[提示词...]

## 镜头 2 | 3秒 | 近景
**转场:** 叠化 | **运镜:** Gentle Dolly In
[提示词...]
```

---

## ✅ 验证规则

所有输出都会通过 5 项检查：

| 规则       | 说明                                       |
| ---------- | ------------------------------------------ |
| Image 编号 | 使用 `Image 1/2/3`，禁用 Subject/Character |
| 语言保留   | 台词保持原语言，不翻译                     |
| 无创意补充 | 严格基于用户输入，不添加内容               |
| 结构正确   | 4段式（Header/Camera/Subject/Environment） |
| 长度限制   | 单镜头 5-8 行                              |

---

## 🔧 自定义

### 添加新的运镜类型

编辑 `resources/knowledge-base.md`，在相应分类下添加。

### 更新平台指南

编辑 `resources/platform-prompts.md`，添加新平台或更新关键词。

### 调整验证规则

编辑 `resources/validation-rules.md`，修改检查项。

---

## 📚 相关文档

- [test.md](test.md) - 原始技术文档
- [CAMERA_DIRECTOR_WORKFLOW.md](CAMERA_DIRECTOR_WORKFLOW.md) - 工作流详解

---

## 版本

**v3.0** - 2026-01-17
- ✅ 双模式支持（单镜头 + 分镜脚本）
- ✅ 九宫格图片处理
- ✅ 三层意图识别
- ✅ 动态知识获取
- ✅ 5 项验证规则
