AI 运镜导演 Skill 实现计划 v3
概述
将 AI 运镜导演工作流程组织成 Claude Code Skill，具备：

双模式支持：单镜头 + 分镜脚本
动态学习能力：指导 AI 使用网络搜索获取最新知识
整合最新研究：Sora/Runway/Pika 提示词结构、专业分镜技术
核心设计：动态学习机制
设计理念
知识库分为静态知识（固定规则）和动态知识（需实时更新），Skill 中明确指导 AI 何时需要搜索最新资料。

触发搜索的场景
搜索触发规则:
  - 用户提到特定 AI 视频工具（Sora, Runway Gen-4, Pika 2.0, Kling）
  - 用户要求"最新"或"最流行"的运镜风格
  - 处理新兴视频类型（VR、沉浸式、垂直短视频）
  - 生成分镜脚本前，搜索目标平台的最佳实践
搜索关键词模板
基础搜索: "[工具名] prompt guide camera movement [年份]"
分镜搜索: "professional storyboard techniques [年份]"
转场搜索: "film transition types [效果类型] cinematography"
Skill 目录结构
.claude/skills/camera-director/
├── SKILL.md                              # 主入口（含动态学习指令）
├── resources/
│   ├── knowledge-base.md                 # 完整运镜知识库
│   ├── platform-prompts.md               # 各平台提示词结构 [NEW]
│   ├── transitions.md                    # 转场类型参考 [NEW]
│   ├── storyboard-guide.md               # 分镜技术指南 [NEW]
│   └── validation-rules.md               # 验证规则
└── workflows/
    ├── single-shot-workflow.md           # 模式A工作流
    └── storyboard-workflow.md            # 模式B工作流
文件内容规划
1. SKILL.md（主入口）
---
name: AI Camera Director
description: 生成专业视频运镜提示词。支持单镜头和分镜脚本。关键词：video prompt, camera movement, 运镜, storyboard, 分镜。
---
核心指令：

# AI Camera Director Skill
## 你的角色
你是专业的视频导演和运镜专家，能够：
1. 分析用户场景，推荐合适的运镜方案
2. 生成符合 AI 视频生成模型的专业提示词
3. 创建完整的分镜脚本
## 动态学习规则（重要！）
### 何时需要搜索
在以下情况下，你应该主动搜索网络获取最新知识：
1. **用户提到特定工具**
   - 搜索: "[工具名] prompt guide camera control [当前年份]"
   - 工具: Sora, Runway Gen-4, Pika, Kling, Vidu, Luma Dream Machine
2. **需要最新趋势**
   - 搜索: "AI video generation best practices [当前年份]"
   - 搜索: "cinematic camera movement trends"
3. **特殊视频类型**
   - 垂直视频: "vertical video cinematography TikTok Reels"
   - VR/360: "360 video camera movement VR"
4. **分镜脚本生成前**
   - 搜索: "professional storyboard shot list techniques"
   - 搜索: "film transition types montage editing"
### 搜索后的整合
- 将新知识与本地知识库结合
- 优先使用平台官方指南
- 标注知识来源供用户参考
## 模式识别
[引用 workflows/single-shot-workflow.md 和 storyboard-workflow.md]
## 核心验证规则
[引用 resources/validation-rules.md]
2. resources/knowledge-base.md
完整运镜知识库（基于最新搜索整合）：

# 运镜知识库
## 一、基础运镜动作
### 1.1 平面运动类 (Planar)
| 英文术语 | 中文 | 动作描述       | 情感表达   | AI提示词关键词                         |
| -------- | ---- | -------------- | ---------- | -------------------------------------- |
| Pan      | 横摇 | 摄像机水平旋转 | 探索、观察 | `panning`, `horizontal pan`            |
| Tilt     | 纵摇 | 摄像机垂直旋转 | 敬畏、压迫 | `tilting`, `vertical tilt`             |
| Truck    | 平移 | 摄像机水平移动 | 陪伴、流畅 | `truck left/right`, `lateral movement` |
| Dolly    | 推拉 | 摄像机前后移动 | 亲密/疏离  | `dolly in/out`, `push in`, `pull back` |
### 1.2 垂直运动类 (Vertical)
| 英文术语 | 中文     | 动作描述           | 情感表达   | AI提示词关键词              |
| -------- | -------- | ------------------ | ---------- | --------------------------- |
| Crane    | 升降     | 垂直升降移动       | 宏大、超越 | `crane up/down`, `jib shot` |
| Pedestal | 底座升降 | 摄像机沿垂直轴升降 | 权力转换   | `pedestal up/down`          |
### 1.3 旋转运动类 (Rotational)
| 英文术语 | 中文 | 动作描述        | 情感表达     | AI提示词关键词                      |
| -------- | ---- | --------------- | ------------ | ----------------------------------- |
| Arc      | 弧形 | 绕主体弧形移动  | 审视、欣赏   | `arc shot`, `curved tracking`       |
| Orbit    | 环绕 | 360度绕主体旋转 | 聚焦、仪式感 | `orbit`, `360 rotation`, `circling` |
| Roll     | 翻滚 | 沿镜头轴旋转    | 混乱、眩晕   | `dutch angle roll`, `camera roll`   |
### 1.4 光学运动类 (Optical)
| 英文术语   | 中文     | 动作描述   | 情感表达   | AI提示词关键词             |
| ---------- | -------- | ---------- | ---------- | -------------------------- |
| Zoom In    | 推镜头   | 焦距拉近   | 紧张、发现 | `zoom in`, `optical zoom`  |
| Zoom Out   | 拉镜头   | 焦距拉远   | 释放、孤独 | `zoom out`, `zooming out`  |
| Rack Focus | 焦点转移 | 改变对焦点 | 发现、暗示 | `rack focus`, `focus pull` |
## 二、复合运镜技法
| 英文术语      | 中文     | 组合方式        | AI提示词关键词                    |
| ------------- | -------- | --------------- | --------------------------------- |
| Dolly Zoom    | 滑动变焦 | 推拉 + 反向变焦 | `dolly zoom`, `vertigo effect`    |
| Tracking Shot | 跟拍     | 平移 + 跟随     | `tracking shot`, `following`      |
| Steadicam     | 斯坦尼康 | 稳定 + 自由移动 | `steadicam`, `smooth tracking`    |
| Whip Pan      | 甩镜头   | 极快横摇        | `whip pan`, `fast pan`            |
| Bullet Time   | 子弹时间 | 多机位定格环绕  | `bullet time`, `time freeze 360`  |
| FPV/POV       | 主观视角 | 第一人称        | `FPV`, `POV shot`, `first person` |
| Dutch Angle   | 荷兰角   | 摄像机倾斜      | `dutch angle`, `tilted frame`     |
## 三、风格修饰词
### 3.1 速度维度
| 修饰词  | 描述     | 适用场景     |
| ------- | -------- | ------------ |
| Slow    | 极慢速   | 情感戏、回忆 |
| Gentle  | 慢速平滑 | 爱情、自然   |
| Smooth  | 匀速     | 广告、时尚   |
| Dynamic | 富有变化 | MV、运动     |
| Fast    | 高速     | 追逐、高潮   |
| Rapid   | 极快     | 爆炸、冲突   |
### 3.2 力度维度
| 修饰词     | 描述         | 适用场景       |
| ---------- | ------------ | -------------- |
| Subtle     | 几乎不可察觉 | 心理戏、氛围   |
| Steady     | 坚定有力     | 纪录、采访     |
| Aggressive | 强烈冲击     | 战斗、极限运动 |
| Sudden     | 突发变化     | 惊悚、反转     |
## 四、场景-运镜匹配矩阵
### 按主体类型
- **人物面部/情感**: Dolly In, Push In, Focus Pull (Style: Slow, Gentle)
- **人物全身/动作**: Tracking, Arc, Truck (Style: Dynamic, Smooth)
- **风景/自然**: Pan, Tilt, Drone Reveal (Style: Slow, Ethereal)
- **动作/运动**: Tracking, Whip Pan, FPV (Style: Fast, Aggressive)
### 按情感氛围
- **浪漫/温馨**: Dolly, Arc, Gentle Pan (Avoid: Aggressive)
- **紧张/悬疑**: Push In, Dutch Angle (Avoid: Smooth)
- **震撼/史诗**: Crane, Drone, Dolly Zoom (Style: Cinematic)
3. resources/platform-prompts.md [NEW]
各平台提示词结构（基于最新搜索）：

# AI 视频生成平台提示词指南
## OpenAI Sora
### 提示词结构（6层框架）
[Scene Summary] + [Camera Shot/Angle] + [Camera Movement] + [Subject & Action] + [Lighting & Color] + [Style & Mood]

### 关键词参考
**镜头类型**: Close-Up, Medium Shot, Wide Shot, Establishing Shot, Over-the-Shoulder
**机位角度**: Low Angle, High Angle, Bird's Eye View, Dutch Angle, Eye-Level
**运动**: Pan, Tilt, Dolly, Tracking, Crane, Zoom, Handheld, Steadicam
**特殊**: Drone shot, POV, Time-lapse, Slow-motion
### 示例
A confident news anchor in a high-tech studio. Medium shot, low angle. Camera slowly dollies in as she delivers breaking news. Soft ambient lighting with blue accent tones. Cinematic documentary style.

---
## Runway Gen-4
### 提示词结构
[Subject Motion] + [Scene Motion] + [Camera Motion] + [Style Descriptor]

### 运动关键词
**相机**: tracking, panning, dolly, orbit, truck right/left
**速度**: low speed (清晰), high speed (可能产生抖动)
**方向**: negative space, open foreground, layered background
### 示例
A cyclist on a coastal road, cliffs and ocean in background, golden hour. Motion: Truck Right, low speed. Cinematic, handheld stability.

---
## Pika Labs
### 关键技巧
1. 高度具体化 - 使用丰富描述词
2. 负面提示词 - 用 `-neg` 排除不想要的元素
3. 参考图片 - 结合图片引导生成
4. 参数控制: `-gs` (引导强度), `-ar` (宽高比), `-seed` (一致性)
### 相机控制参数
- `motion_control` - 精确动画控制
- 方向指定: zoom in/out, pan left/right, rotate
---
## 通用最佳实践
1. **单一运动原则**: 每个镜头只指定一个主运镜 + 一个主动作
2. **正面描述**: 描述想要什么，而非不想要什么
3. **时间节拍**: 复杂场景按时间段拆分 [0-2s], [2-4s]
4. **迭代优化**: 从简单开始，逐步添加细节
4. resources/transitions.md [NEW]
转场类型参考（用于分镜脚本）：

# 电影转场类型指南
## 基础转场
| 类型 | 英文     | 效果描述           | 情感/叙事作用      | 使用场景         |
| ---- | -------- | ------------------ | ------------------ | ---------------- |
| 硬切 | Cut      | 直接切换           | 自然流畅、推进情节 | 最常用、对话场景 |
| 跳切 | Jump Cut | 同场景时间跳跃     | 紧迫感、时间流逝   | 快节奏剪辑       |
| L切  | L-Cut    | 画面先切，声音延续 | 平滑过渡           | 对话场景         |
| J切  | J-Cut    | 声音先切，画面后切 | 预示下一场景       | 悬念铺垫         |
## 渐变转场
| 类型 | 英文     | 效果描述       | 情感/叙事作用  | 使用场景         |
| ---- | -------- | -------------- | -------------- | ---------------- |
| 叠化 | Dissolve | 两画面重叠渐变 | 时间流逝、回忆 | 时空转换、蒙太奇 |
| 淡入 | Fade In  | 从黑/白渐现    | 开始、觉醒     | 开场、新段落     |
| 淡出 | Fade Out | 渐变至黑/白    | 结束、沉睡     | 结尾、章节结束   |
## 特殊转场
| 类型     | 英文         | 效果描述          | 情感/叙事作用      | 使用场景     |
| -------- | ------------ | ----------------- | ------------------ | ------------ |
| 擦除     | Wipe         | 新画面"擦"过      | 时空跳跃、场景切换 | 星球大战风格 |
| 圆形擦除 | Iris Wipe    | 圆圈缩放擦除      | 复古、喜剧         | 老电影风格   |
| 匹配剪辑 | Match Cut    | 视觉/动作相似衔接 | 深层关联、象征     | 艺术表达     |
| 声音桥接 | Sound Bridge | 声音跨场景延续    | 平滑过渡           | 叙事连续性   |
## 分镜脚本中的转场标注
镜头 1 (3s) → [Dissolve] → 镜头 2 (2s) 镜头 2 (2s) → [Cut] → 镜头 3 (4s) 镜头 3 (4s) → [Fade Out] → 结束

5. resources/storyboard-guide.md [NEW]
专业分镜技术指南：

# 分镜脚本创作指南
## 分镜规划要素
### 1. 镜头类型分布
- **开场**: 通常使用 Establishing Shot (远景) 建立场景
- **发展**: Medium Shot / Close-up 推进叙事
- **高潮**: 动态运镜 + 特写 强化情感
- **结尾**: 远景或渐变结束
### 2. 景别节奏公式
远景 → 中景 → 近景 → 特写 → 中景 → 远景 (建立) (交代) (聚焦) (高潮) (缓冲) (结束)

### 3. 时长建议
| 镜头类型      | 建议时长 | 说明           |
| ------------- | -------- | -------------- |
| 远景/建立镜头 | 3-5秒    | 让观众理解环境 |
| 中景          | 2-4秒    | 标准叙事节奏   |
| 近景/特写     | 1-3秒    | 短促有力       |
| 动作镜头      | 2-4秒    | 根据动作复杂度 |
| 情感镜头      | 3-5秒    | 留给观众消化   |
## 分镜脚本模板
```markdown
# [项目名称] 分镜脚本
**总时长**: XX秒 | **镜头数**: X | **风格**: [风格描述]
---
## 镜头 1 | [时长]秒 | [景别]
**转场**: [淡入/切换/叠化]
**运镜**: [运镜类型 + 修饰词]
**AI提示词**:
[完整的视频生成提示词]

**备注**: [特殊说明]
---
叙事结构模式
三幕式 (3-5张图)
开端 (1-2镜头): 建立场景和人物
发展 (2-3镜头): 冲突或情感展开
结局 (1镜头): 解决或开放式结尾
蒙太奇式 (5-9张图)
无明确叙事线
通过视觉关联或主题统一
常用于MV、广告、情绪短片
故事式 (7-12张图)
开场建立
人物介绍
事件触发
发展
高潮
结局
(可选) 尾声
---
## 工作流更新
### workflows/single-shot-workflow.md
（保持原有 Step 1-3，添加动态学习检查点）
### workflows/storyboard-workflow.md
```markdown
# 分镜脚本工作流
## 前置检查：动态学习
如果用户指定了目标平台（Sora/Runway/Pika等），先搜索：
- `[平台名] prompt guide [当前年份]`
- `[平台名] camera movement keywords`
## Step B1: 分镜规划
### 输入分析
1. 统计图片数量
2. 识别叙事类型（三幕式/蒙太奇/故事式）
3. 分析图片内容，推断叙事顺序
4. 检测情感基调
### 结构规划
1. 分配每镜头景别（远→近→远）
2. 规划时长分布
3. 选择转场类型
4. 确定整体风格
### 输出
```json
{
  "total_duration": "25秒",
  "shot_count": 9,
  "style": "文艺/慢节奏",
  "structure": [
    {"shot": 1, "type": "establishing", "duration": "3s", "transition": "fade_in"},
    {"shot": 2, "type": "medium", "duration": "2s", "transition": "cut"},
    ...
  ]
}
Step B2: 循环生成
对每张图执行：

Step 1: 分析约束
Step 2: 推荐运镜（结合分镜规划的景别要求）
Step 3: 生成提示词
额外添加：

镜头编号
转场标注
时长标注
Step B3: 整合输出
按 storyboard-guide.md 模板格式化输出完整分镜脚本。

---
## 实施步骤
1. 创建目录 `.claude/skills/camera-director/`
2. 编写 `SKILL.md`（含动态学习指令）
3. 编写 `resources/knowledge-base.md`
4. 编写 `resources/platform-prompts.md` [NEW]
5. 编写 `resources/transitions.md` [NEW]
6. 编写 `resources/storyboard-guide.md` [NEW]
7. 编写 `resources/validation-rules.md`
8. 编写 `workflows/single-shot-workflow.md`
9. 编写 `workflows/storyboard-workflow.md`
---
## 验证测试
| 测试场景                  | 预期行为                 |
| ------------------------- | ------------------------ |
| "用 Runway Gen-4 生成..." | 触发搜索 Runway 最新指南 |
| 9 张图 + "帮我做分镜"     | 模式 B + 搜索分镜技术    |
| "最新的运镜趋势"          | 搜索当前年份趋势         |
| 单张图 + 场景描述         | 模式 A，使用本地知识库   |
