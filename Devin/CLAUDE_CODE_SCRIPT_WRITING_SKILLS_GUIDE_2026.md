# GitHub Claude Code 剧本与提示词开发技能指南 2026

**利用 Claude Code 和开源技能库开发专业剧本和提示词**

**创建日期：** 2026 年 4 月 19 日  
**目标：** 发现和使用 GitHub 上最佳的 Claude Code 剧本创作和提示词工程技能

---

## 🎯 执行摘要

### 核心发现

**最大 Claude Code 技能库：**
- **alirezarezvani/claude-skills**: 235+ 生产就绪技能
- **ComposioHQ/awesome-claude-skills**: 精选技能列表
- **ckelsoe/prompt-architect**: 27 种提示词框架
- 支持 12+ AI 编码工具（Claude Code, Cursor, Gemini CLI 等）

**剧本创作相关技能：**
```
✅ 内容创作技能（44 个营销技能）
✅ 提示词工程工具包
✅ 角色和叙事生成
✅ 多语言内容生成
✅ 品牌声音和风格指南
```

**提示词工程框架：**
```
✅ CO-STAR（内容创作）
✅ RISEN（多步骤流程）
✅ RACE（专家任务）
✅ TIDD-EC（高精度任务）
✅ 链式思维（推理任务）
```

---

## 📚 第一部分：顶级 GitHub 仓库

### 1. alirezarezvani/claude-skills ⭐⭐⭐⭐⭐

**仓库信息：**
```
URL: https://github.com/alirezarezvani/claude-skills
Stars: 5,200+
技能数：235+
支持工具：12 个（Claude Code, Cursor, Gemini CLI 等）
许可：MIT
```

**剧本创作相关技能：**

| 技能类别 | 技能数 | 相关用途 |
|---------|--------|---------|
| **Marketing Skills** | 44 | 内容创作、SEO、转化文案 |
| **Content Production** | 8 | 博客文章、社交媒体内容 |
| **Copywriting** | 6 | 销售文案、广告文案 |
| **Product Team** | 16 | 产品故事、用户场景 |
| **C-Level Advisory** | 34 | 战略叙事、商业故事 |

**安装方法：**
```bash
# 克隆仓库
git clone https://github.com/alirezarezvani/claude-skills.git
cd claude-skills

# Claude Code 安装
cp -r marketing-skill ~/.claude/skills/
cp -r product-team ~/.claude/skills/

# 或使用插件系统
/plugin marketplace add alirezarezvani/claude-skills
/plugin install marketing-skills@claude-code-skills
```

**关键技能示例：**

**1. Content Creator**
```markdown
用途：生成博客文章、社交媒体内容、视频脚本
功能：
- SEO 优化
- 品牌声音匹配
- 多平台格式适配
- A/B 测试变体生成
```

**2. Prompt Engineer Toolkit**
```markdown
用途：优化提示词质量
功能：
- 提示词 A/B 测试
- 提示词版本管理
- 提示词差异对比
- 最佳实践应用
```

**3. Brand Guidelines**
```markdown
用途：确保内容符合品牌标准
功能：
- 品牌颜色应用
- 字体和排版
- 视觉识别一致性
- 专业设计标准
```

---

### 2. ComposioHQ/awesome-claude-skills ⭐⭐⭐⭐

**仓库信息：**
```
URL: https://github.com/ComposioHQ/awesome-claude-skills
类型：精选技能列表
特色：可连接 500+ 应用执行实际动作
```

**剧本创作相关技能：**

| 技能 | 用途 | 特色 |
|------|------|------|
| **Internal Comms** | 内部通讯写作 | 公司特定格式 |
| **Lead Research** | 潜在客户研究 | 行动策略生成 |
| **Competitive Ads** | 竞品广告分析 | 创意方法提取 |
| **Domain Brainstorm** | 域名头脑风暴 | 多 TLD 可用性检查 |
| **Skill Creator** | 创建新技能 | 技能开发指导 |

**安装方法：**
```bash
# 连接应用插件
git clone https://github.com/ComposioHQ/awesome-claude-skills.git
cd awesome-claude-skills/connect-apps-plugin

# 设置连接
claude --plugin-dir ./connect-apps-plugin
/connect-apps:setup
# 粘贴 API key（platform.composio.dev 获取）
```

---

### 3. ckelsoe/prompt-architect ⭐⭐⭐⭐⭐

**仓库信息：**
```
URL: https://github.com/ckelsoe/prompt-architect
框架数：27 种研究支持的框架
特色：将模糊提示词转换为专家级结构化提示词
```

**27 种提示词框架分类：**

| 复杂度 | 框架 | 最佳用途 |
|--------|------|---------|
| **高** | CO-STAR | 内容创作、写作任务 |
| **高** | RISEN | 多步骤流程、程序 |
| **高** | CRISPE | 多输出变体 |
| **中** | BROKE | 商业交付（OKR 风格） |
| **中** | RISE-IE | 数据分析、转换 |
| **中** | TIDD-EC | 高精度任务（明确 Do's/Don'ts） |
| **中** | RACE | 专家任务 |
| **中** | Chain of Thought | 推理、问题解决 |
| **低** | RTF | 简单任务 |
| **低** | APE | 超简单一次性提示 |

**安装方法：**
```bash
# 交互式安装（推荐）
npx @ckelsoe/prompt-architect

# 自动检测 AI 工具并选择安装位置
# 支持：Claude Code, Gemini CLI, Cursor, Copilot 等
```

**使用示例：**

**输入（模糊提示词）：**
```
"Write about machine learning"
```

**分析评分：**
```
- Clarity: 2/10
- Specificity: 1/10
- Context: 0/10
- Completeness: 2/10
- Structure: 3/10
- Overall: 1.6/10
```

**输出（CO-STAR 框架优化后）：**
```markdown
CONTEXT:
Creating content for a business blog aimed at C-level executives 
exploring how AI/ML could benefit their organizations. Readers 
understand business strategy but have limited technical ML knowledge.

OBJECTIVE:
Create an engaging article helping executives understand practical 
machine learning applications. Focus on tangible business value.

STYLE:
Professional blog style with narrative and bullet points. Include 
2-3 real-world case studies. Clear subheadings every 150-200 words.

TONE:
Professional yet approachable. Confident without being condescending. 
Practical and business-focused.

AUDIENCE:
C-suite executives and senior managers at mid-to-large enterprises.

RESPONSE FORMAT:
800-word article with:
- Compelling headline (10 words max)
- Brief hook (2-3 sentences)
- 3-4 main sections with subheadings
- Clear call-to-action conclusion
```

**优化后评分：**
```
- Clarity: 9/10
- Specificity: 9/10
- Context: 10/10
- Completeness: 9/10
- Structure: 9/10
- Overall: 8.8/10
```

---

### 4. 其他重要仓库

**ThamJiaHe/claude-prompt-engineering-guide**
```
URL: https://github.com/ThamJiaHe/claude-prompt-engineering-guide
特色：Claude 4.x 模型官方最佳实践
内容：Skills, Plugins, MCP, Hooks, Agent Teams, 100+ 精选技能
```

**shanraisshan/claude-code-best-practice**
```
URL: https://github.com/shanraisshan/claude-code-best-practice
特色：从 Vibe Coding 到 Agentic Engineering
关键建议：
- Skill description 是触发器，不是总结
- 不要给 Claude 规定步骤，给目标和约束
- 在技能中包含脚本和库
- 使用 !command 注入动态 shell 输出
```

**Piebald-AI/claude-code-system-prompts**
```
URL: https://github.com/Piebald-AI/claude-code-system-prompts
内容：
- Claude Code 完整系统提示词
- 24 个内置工具描述
- 子 Agent 提示词（Plan/Explore/Task）
- 每日更新每个 Claude Code 版本
```

---

## 🎬 第二部分：剧本创作技能应用

### 短剧剧本开发工作流

**使用技能组合：**
```
1. Content Creator → 生成初稿
2. Prompt Architect → 优化提示词
3. Brand Guidelines → 确保风格一致
4. Self-Improving Agent → 从反馈学习
```

**示例工作流：**

**步骤 1: 使用 CO-STAR 框架创建剧本提示词**
```markdown
CONTEXT:
Creating a 10-episode Chinese wisdom short drama series based on 
36 Strategies. Target audience: global viewers interested in 
business strategy and Eastern philosophy. Each episode 90-120 seconds.

OBJECTIVE:
Write Episode 1 script that hooks viewers in first 5 seconds, 
builds tension, and ends with cliffhanger. Demonstrate "Deceive 
the Heavens" strategy in modern tech startup context.

STYLE:
Vertical video format (9:16). Fast-paced, emotionally intense. 
Mix of dialogue and visual storytelling. Show don't tell.

TONE:
Suspenseful, inspiring, with moments of strategic brilliance. 
Eastern wisdom meets Western business drama.

AUDIENCE:
25-45 year old professionals, entrepreneurs, business students. 
Global audience (English subtitles). Familiar with shows like 
Succession, Billions, but want fresh perspective.

RESPONSE FORMAT:
90-second script with:
- Scene headings (INT./EXT., location, time)
- Character names and brief descriptions
- Dialogue (concise, impactful)
- Visual directions (camera angles, key actions)
- Timing notes for each beat
- Cliffhanger ending
```

**步骤 2: 使用 RISEN 框架优化多集架构**
```markdown
ROLE:
Expert short drama showrunner with 10+ years experience creating 
viral vertical series for ReelShort, DramaBox platforms.

INSTRUCTIONS:
Create 10-episode season arc for "36 Strategies: Tech Wars" series. 
Each episode must end with cliffhanger. Overall season tells complete 
story of underdog startup defeating tech giant using ancient wisdom.

STEPS:
1. Define protagonist's goal and main obstacle
2. Map antagonist's power and vulnerabilities  
3. Plan which strategy each episode demonstrates
4. Build escalating stakes across episodes
5. Design mid-season twist (episode 5-6)
6. Create season finale setup
7. Plant seeds for season 2

END GOAL:
10-episode outline with episode titles, 1-sentence summaries, 
and cliffhanger descriptions. Ready for scriptwriting.

NARROWING:
- Each episode 90-120 seconds when produced
- Budget: AI production (no physical filming constraints)
- Cast: 5 main characters max (AI consistency limits)
- Locations: 3-4 recurring settings
```

---

### 角色开发技能

**使用 Product Team 技能：**

**技能：UX Researcher**
```markdown
用途：创建深度角色档案
提示词示例：

"Using UX researcher methodology, create detailed character profiles 
for our 36 Strategies short drama:

Protagonist (Li Ming, 35):
- Background: Tech entrepreneur, previously betrayed
- Motivation: Complete father's unfinished mission
- Strengths: Strategic thinking, resilience
- Weaknesses: Trust issues, works alone
- Arc: From lone wolf to team builder

Antagonist (CEO Zhang, 50):
- Background: Built empire through ruthless tactics
- Motivation: Maintain market dominance
- Strengths: Resources, connections, experience
- Weaknesses: Underestimates young competitors
- Arc: From overconfident to desperate

For each character, provide:
- Physical description (for AI video generation)
- Speech patterns and catchphrases
- Key relationships
- Episode-by-episode evolution"
```

**技能：Product Manager Toolkit**
```markdown
用途：故事线优先级排序
工具：RICE 优先级评分脚本

python3 product-team/product-manager-toolkit/scripts/rice_prioritizer.py storylines.csv

输出：
- Reach: 多少观众会受影响
- Impact: 情感冲击力
- Confidence: 成功信心
- Effort: 制作难度
- RICE Score: 综合优先级
```

---

### 多语言内容生成

**使用 Marketing Skills：**

**技能：Content Production**
```markdown
用途：多语言剧本适配
Python 工具：brand_voice_analyzer.py

# 分析品牌声音
python3 marketing-skill/content-production/scripts/brand_voice_analyzer.py chinese_script.txt

输出：
- 语气分析
- 情感基调
- 文化参考点
- 本地化建议
```

**本地化工作流：**
```
中文原版 → 英文适配 → 其他语言

关键考虑：
1. 三十六计名称翻译
   - 瞒天过海 → "Deceive the Heavens"
   - 围魏救赵 → "Besiege Wei to Rescue Zhao"
   
2. 文化背景解释
   - 添加简短字幕说明
   - 视觉化而非对话解释
   
3. 对话节奏调整
   - 英文更直接
   - 中文更含蓄
   - 调整但不失原味
```

---

## 🛠️ 第三部分：提示词工程框架详解

### CO-STAR 框架（内容创作）

**适用场景：**
- 博客文章、剧本、营销文案
- 需要完整背景的内容
- 多平台内容适配

**框架结构：**
```
C - Context（背景）
  - 情况描述
  - 相关信息
  - 约束条件

O - Objective（目标）
  - 清晰目标
  - 成功标准
  - 关键结果

S - Style（风格）
  - 写作风格
  - 格式方法
  - 参考示例

T - Tone（语气）
  - 声音特质
  - 情感质量
  - 关系定位

A - Audience（受众）
  - 目标读者特征
  - 知识水平
  - 期望和需求

R - Response（响应格式）
  - 输出结构
  - 长度要求
  - 格式规范
```

**剧本创作模板：**
```markdown
CONTEXT:
[项目背景、系列定位、平台要求]

OBJECTIVE:
[本集目标、情感目标、观众反应]

STYLE:
[叙事风格、视觉风格、参考作品]

TONE:
[情感基调、节奏、氛围]

AUDIENCE:
[目标观众画像、文化背景]

RESPONSE:
[剧本格式、时长、特殊要求]
```

---

### RISEN 框架（多步骤流程）

**适用场景：**
- 多集故事架构
- 系列规划
- 复杂角色开发

**框架结构：**
```
R - Role（角色）
  - 需要的专业知识
  - 视角和立场

I - Instructions（指令）
  - 高级指导
  - 方向性建议

S - Steps（步骤）
  - 详细方法
  - 执行流程

E - End Goal（最终目标）
  - 成功标准
  - 交付物

N - Narrowing（约束）
  - 限制条件
  - 边界定义
```

**季架构模板：**
```markdown
ROLE:
Expert showrunner with 10+ years creating viral short drama series.

INSTRUCTIONS:
Plan 100-episode season arc for Chinese wisdom business drama.
Each episode 90-120 seconds, must end with cliffhanger.

STEPS:
1. Define core conflict and protagonist goal
2. Map antagonist power structure
3. Assign 36 Strategies to episode groups
4. Plan escalation points (ep 10, 25, 50, 75)
5. Design mid-season twist
6. Build to season finale
7. Plant season 2 seeds

END GOAL:
100-episode outline with titles, summaries, cliffhangers.

NARROWING:
- AI production constraints (5 characters max, 4 locations)
- Budget: $2000 total
- Timeline: 35 days
- Platforms: ReelShort, DramaBox, TikTok
```

---

### TIDD-EC 框架（高精度任务）

**适用场景：**
- 需要明确边界的任务
- 质量关键型内容
- 合规要求

**框架结构：**
```
T - Task Type（任务类型）
  - 工作性质
  - 分类

I - Instructions（指令）
  - 要完成什么

D - Do（要做）
  - 明确正面指导
  - 最佳实践

D - Don't（不做）
  - 明确负面指导
  - 避免什么

E - Examples（示例）
  - 参考样本
  - 质量标准

C - Context（背景）
  - 相关信息
```

**剧本质量检查模板：**
```markdown
TASK TYPE:
Short drama script quality audit and optimization.

INSTRUCTIONS:
Review episode script against viral short drama best practices.
Identify weaknesses and provide specific improvements.

DO:
- Analyze first 5-second hook effectiveness
- Check cliffhanger strength
- Verify emotional arc
- Ensure visual storytelling
- Validate pacing for 90-second format
- Check character consistency

DON'T:
- Don't suggest expensive production changes
- Don't add complex camera movements
- Don't increase character count
- Don't extend beyond 120 seconds
- Don't add exposition dialogue

EXAMPLES:
[Provide 2-3 successful episode scripts as reference]

CONTEXT:
Episode 3 of 100-episode series. Previous episodes established 
conflict. This episode must escalate stakes while maintaining 
character consistency for AI video generation.
```

---

## 📊 第四部分：技能组合推荐

### 短剧制作完整技能栈

**前期制作：**
```
1. Prompt Architect → 优化所有提示词
2. Content Creator → 生成剧本初稿
3. UX Researcher → 深度角色开发
4. Product Manager → 故事线优先级
```

**制作阶段：**
```
5. Brand Guidelines → 视觉一致性
6. Self-Improving Agent → 从反馈学习
7. Test-Driven Development → 质量检查
```

**后期制作：**
```
8. Content Production → 多语言适配
9. Internal Comms → 营销材料
10. Lead Research → 受众研究
```

---

### 安装和配置

**完整安装脚本：**
```bash
#!/bin/bash
# Claude Code 短剧创作技能安装

echo "Installing Claude Code Skills for Short Drama Production..."

# 1. 克隆主要技能库
git clone https://github.com/alirezarezvani/claude-skills.git
cd claude-skills

# 2. 安装到 Claude Code
cp -r marketing-skill ~/.claude/skills/
cp -r product-team ~/.claude/skills/
cp -r c-level-advisor ~/.claude/skills/

# 3. 安装 Prompt Architect
npx @ckelsoe/prompt-architect

# 4. 验证安装
echo "Verifying installation..."
ls -la ~/.claude/skills/ | grep -E "marketing|product|c-level"

# 5. 创建快捷方式
cat >> ~/.zshrc << 'EOF'
# Claude Code Short Drama Skills
alias drama-creator="claude --skill content-creator"
alias prompt-optimize="claude --skill prompt-architect"
alias brand-check="claude --skill brand-guidelines"
EOF

source ~/.zshrc

echo "✅ Installation complete!"
echo ""
echo "Quick Start:"
echo "1. claude --skill content-creator"
echo "2. Use CO-STAR framework for script writing"
echo "3. Use RISEN for season planning"
echo "4. Use TIDD-EC for quality checks"
```

---

## 🎯 第五部分：实战示例

### 示例 1: 使用 CO-STAR 创作开场镜头

**输入提示词：**
```markdown
CONTEXT:
Tech startup drama, Episode 1 opening scene. Need to hook viewers 
in first 5 seconds. Modern office setting, board room confrontation.

OBJECTIVE:
Create opening scene that immediately establishes conflict, shows 
protagonist's vulnerability, and makes viewers curious about what 
happens next.

STYLE:
Vertical video (9:16). Quick cuts between character reactions. 
Visual storytelling over dialogue.

TONE:
Tense, dramatic, with underlying mystery.

AUDIENCE:
Mobile viewers with short attention spans. Must grab immediately 
or they scroll away.

RESPONSE:
30-second opening scene script with:
- Shot-by-shot breakdown
- Dialogue (minimal)
- Visual directions
- Timing for each shot
```

**Claude 输出：**
```markdown
EPISODE 1 - OPENING SCENE (30 seconds)

SHOT 1 (0-3s): EXTREME CLOSE-UP
Li Ming's eyes widening in shock. Reflection of projector screen 
in his glasses showing "TERMINATED" in red letters.
SOUND: Sharp inhale

SHOT 2 (3-7s): WIDE SHOT
Board room. 10 executives staring at Li Ming. CEO at head of 
table, cold expression.
CEO: "All evidence points to you, Li Ming."

SHOT 3 (7-12s): MEDIUM SHOT
Li Ming's hands gripping chair arms. Knuckles white.
LI MING: "This is insane. I would never—"
CEO: (interrupts) "Security."

SHOT 4 (12-18s): TRACKING SHOT
Two guards approach. Camera follows Li Ming standing up slowly.
LI MING: (quietly) "You'll regret this."

SHOT 5 (18-25s): OVER-THE-SHOULDER
Li Ming walking to door. Stops, looks back.
LI MING: "Three months. That's all you have."

SHOT 6 (25-30s): CLOSE-UP
CEO's face. First hint of uncertainty.
CUT TO BLACK.
TITLE CARD: "DECEIVE THE HEAVENS"

END OPENING
```

---

### 示例 2: 使用 RISEN 规划 10 集架构

**输入提示词：**
```markdown
ROLE:
Experienced short drama showrunner. Created 5+ viral series with 
100M+ total views. Expert in vertical format storytelling.

INSTRUCTIONS:
Plan 10-episode season arc for "36 Strategies: Tech Wars". 
Each episode must end with cliffhanger. Overall story: underdog 
startup defeats tech giant using ancient Chinese wisdom.

STEPS:
1. Define protagonist's goal and main obstacle
2. Map antagonist's power and vulnerabilities
3. Assign strategies to episode groups (1-3, 4-6, 7-9, 10)
4. Build escalating stakes
5. Design mid-season twist (episode 5)
6. Create finale setup
7. Plant season 2 seeds

END GOAL:
10-episode outline with:
- Episode titles
- 1-sentence summaries
- Cliffhanger descriptions
- Strategy demonstrated

NARROWING:
- AI production: 5 characters max, 4 locations
- Each episode 90-120 seconds
- Budget: $2000 total
- Platforms: ReelShort, DramaBox
```

**Claude 输出（摘要）：**
```markdown
SEASON 1 ARC: "Deceive the Heavens"

EPISODE 1: "Betrayal"
Summary: Li Ming fired, accused of stealing core technology.
Cliffhanger: Mysterious person offers help, "B Plan activated."
Strategy: Setting up the deception

EPISODE 2: "Undercurrent"
Summary: Li Ming's team works in secret lab while competitor 
announces "breakthrough" product.
Cliffhanger: Message about Li Ming's father's past.
Strategy: Hidden preparation

EPISODE 3: "Father's Secret"
Summary: Reveals father was similarly framed years ago. Left 
notebook with industry truths.
Cliffhanger: "That person" still controls the industry.
Strategy: Learning from past

EPISODE 4-5: "Allies and Enemies"
[Young engineer contacts Li Ming, offers inside data]
[Li Ming must decide: expose or wait?]
MID-SEASON TWIST: Engineer's true identity revealed

EPISODE 6-8: "The Trap"
[Li Ming sacrifices position to save engineer]
[Location exposed, chase sequence]
[Core code complete, needs test data]

EPISODE 9: "Infiltration"
[Break into competitor's server]
[Get data, barely escape]
[All ready for tomorrow's industry conference]

EPISODE 10: "Reversal"
[Competitor's demo fails publicly]
[Li Ming launches mature product]
[CEO: "When did you start?"]
[Li Ming: "From the day you first refused me"]
FINAL CLIFFHANGER: True mastermind revealed (Season 2 setup)
```

---

## 📈 第六部分：质量检查和优化

### 使用 Self-Improving Agent

**技能信息：**
```
位置：engineering-team/self-improving-agent
功能：自动记忆管理、模式提升、技能提取
```

**使用示例：**
```markdown
/activate_skill self-improving-agent

任务：从观众反馈中学习优化剧本

步骤：
1. 收集前 3 集观众评论
2. 分析正面/负面反馈模式
3. 提取成功元素和失败元素
4. 更新后续集创作指南
5. 测试优化后的剧本

输出：
- 观众偏好报告
- 优化建议列表
- A/B 测试方案
```

---

### 使用 Test-Driven Development

**技能信息：**
```
位置：obra/superpowers/skills/test-driven-development
用途：在写实现代码前先写测试
适配：剧本质量检查
```

**剧本测试模板：**
```markdown
在写剧本前，先定义成功标准：

测试 1: 前 5 秒留存
- 标准：70%+ 观众看完前 5 秒
- 检查：开场有冲突/悬念/视觉冲击吗？

测试 2: 完播率
- 标准：50%+ 观众看完
- 检查：每 15 秒有新钩子吗？

测试 3: 付费转化
- 标准：5%+ 观众付费解锁下一集
- 检查：结尾悬念足够强吗？

测试 4: 分享率
- 标准：10%+ 观众分享
- 检查：有情感共鸣点吗？

使用这些测试指导剧本创作，而非事后检查。
```

---

## 🚀 第七部分：快速开始指南

### 30 分钟启动流程

**第 1-5 分钟：安装核心技能**
```bash
# 快速安装
git clone https://github.com/alirezarezvani/claude-skills.git
cd claude-skills
cp -r marketing-skill ~/.claude/skills/
npx @ckelsoe/prompt-architect
```

**第 6-15 分钟：学习框架**
```markdown
阅读 Prompt Architect 文档
- CO-STAR 框架（内容创作）
- RISEN 框架（多步骤流程）
- TIDD-EC 框架（高精度任务）

每个框架练习 1 次
```

**第 16-25 分钟：创作测试剧本**
```markdown
使用 CO-STAR 创作 30 秒开场
使用 RISEN 规划 5 集架构
使用 TIDD-EC 质量检查
```

**第 26-30 分钟：优化和迭代**
```markdown
激活 Self-Improving Agent
从测试反馈学习
优化提示词和剧本
```

---

## 📋 第八部分：最佳实践

### 提示词编写原则

**来自 shanraisshan/claude-code-best-practice：**

```
✅ DO:
- Skill description 是触发器，不是总结
  "当需要 X 时使用" 而非 "这个技能做 X"
- 给目标和约束，而非规定步骤
- 在技能中包含脚本和库
- 使用 !command 注入动态输出

❌ DON'T:
- 不要陈述显而易见的内容
- 不要给 Claude 规定逐步指令
- 不要重复 Claude 默认行为
- 不要让技能过于复杂（聚焦特定场景）
```

---

### 技能组合使用

**Orchestration 模式：**
```markdown
Solo Sprint（单人冲刺）：
- 侧项目、MVP、 solo 创始人
- 在不同阶段切换角色

Domain Deep-Dive（领域深入）：
- 架构审查、合规审计
- 一个角色 + 多个叠加技能

Multi-Agent Handoff（多 Agent 交接）：
- 高风险决策、发布准备
- 角色互相审查输出

Skill Chain（技能链）：
- 内容管道、可重复清单
- 顺序技能，无需角色
```

**示例：6 周产品发布**
```
Week 1-2: startup-cto + aws-architect + senior-frontend → 构建
Week 3-4: growth-marketer + launch-strategy + copywriting → 准备
Week 5-6: solo-founder + email-sequence + analytics → 发布
```

---

## 📖 第九部分：资源链接

### 核心仓库

| 仓库 | URL | 用途 |
|------|-----|------|
| **claude-skills** | github.com/alirezarezvani/claude-skills | 235+ 技能库 |
| **awesome-claude-skills** | github.com/ComposioHQ/awesome-claude-skills | 精选列表 |
| **prompt-architect** | github.com/ckelsoe/prompt-architect | 27 种框架 |
| **claude-prompt-engineering-guide** | github.com/ThamJiaHe/claude-prompt-engineering-guide | 官方最佳实践 |
| **claude-code-best-practice** | github.com/shanraisshan/claude-code-best-practice | 实践指南 |
| **claude-code-system-prompts** | github.com/Piebald-AI/claude-code-system-prompts | 系统提示词 |

### 学习资源

| 资源 | URL | 类型 |
|------|-----|------|
| **Anthropic Prompt Tutorial** | github.com/anthropics/prompt-eng-interactive-tutorial | 官方教程 |
| **Agent Skills** | agentskills.io | 开放标准 |
| **Composio** | composio.dev | 应用连接 |

---

## 🎓 结论：成功要素

### 核心建议

**1. 从简单开始**
```
先掌握 1-2 个框架（CO-STAR, RISEN）
熟练使用 3-5 个核心技能
逐步扩展到复杂工作流
```

**2. 迭代优化**
```
每次使用记录什么有效/无效
使用 Self-Improving Agent 学习
建立个人提示词库
```

**3. 组合使用**
```
单一技能效果有限
技能组合产生协同效应
角色 + 技能 + 工作流 = 最大价值
```

**4. 持续学习**
```
关注 GitHub 仓库更新
参与社区讨论
分享自己的技能和经验
```

---

**最后更新：** 2026 年 4 月 19 日  
**来源：** GitHub 开源技能库、Anthropic 官方文档、社区最佳实践
