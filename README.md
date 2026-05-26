# 🎯 TRAE Skill 创作赛 - 作品提交

## 📅 投稿时间
2025年05月25日 - 05月29日

## 👤 作者信息
- **作者**: fupengyu1
- **平台**: TRAE (https://trae.ai)

---

## 📦 作品列表

### 作品一：WeChat Article Scraper

### 作品二：Habit Tracker

---

## 📝 作品一详解：WeChat Article Scraper

### 1️⃣ Skill 介绍

**WeChat Article Scraper** 是一款专门用于抓取微信公众号文章全文的 Skill。

#### 核心功能
- 📰 抓取微信公众号文章全文内容
- 🖼️ 自动处理微信懒加载图片（`data-src` → Markdown 图片格式）
- 📄 输出干净的 Markdown 格式
- 🔄 支持批量处理

#### 技术亮点
- 使用 Python requests + regex 实现
- 智能识别并提取 `data-src` 属性中的真实图片地址
- 自动清理 HTML 标签，保留纯文本格式
- 输出标准 Markdown，可直接用于笔记软件

### 2️⃣ 使用场景

| 场景 | 说明 |
|------|------|
| 📚 内容采集 | 批量采集竞品公众号文章，做内容分析 |
| 📖 离线阅读 | 将文章保存为 Markdown，随时离线阅读 |
| ✍️ 素材收集 | 内容创作者收集素材和参考资料 |
| 🔍 文章摘要 | 抓取后配合 AI 生成摘要和分析 |

### 3️⃣ 使用 SOLO 的创作过程

```
Step 1: 分析需求
├── 痛点：微信文章无法直接复制，带图片的文章更难处理
├── 目标：提取完整文章内容，包括懒加载图片
└── 方案：Python 脚本 + 正则表达式提取

Step 2: 技术实现
├── 使用 requests 获取页面 HTML
├── 用正则提取 <div id="js_content"> 内容区
├── 替换 <img data-src="xxx"> 为 ![image](xxx)
└── 清理 HTML 标签，输出 Markdown

Step 3: 封装为 Skill
├── 定义 trigger keywords
├── 编写使用说明和示例代码
└── 添加限制说明和注意事项
```

### 4️⃣ 调用步骤

#### 方式一：直接提供 URL
```
用户：帮我抓取这个微信公众号文章 https://mp.weixin.qq.com/s/xxxxx
SOLO：调用 wechat_article_scraper skill
```

#### 方式二：Python 脚本调用
```python
# 保存为 fetch_wx.py
import requests
import re

url = "https://mp.weixin.qq.com/s/xxxxx"
headers = {"User-Agent": "Mozilla/5.0..."}

response = requests.get(url, headers=headers)
html = response.text

# 提取标题和内容
title = re.search(r'property="og:title" content="([^"]+)"', html)
content = re.search(r'<div.*?id="js_content".*?>(.*?)</div>', html, re.DOTALL)

# 处理图片和输出 Markdown
...
```

### 5️⃣ 效果展示

**输入**：微信公众号文章链接

**输出**：
```markdown
# 文章标题

正文内容第一段...

![image](https://mmbiz.qpic.cn/...)

正文内容第二段...

![image](https://mmbiz.qpic.cn/...)
```

### 6️⃣ Skill 链接

> 📍 安装路径：`.trae/skills/wechat_article_scraper/SKILL.md`

---

## 📝 作品二详解：Habit Tracker

### 1️⃣ Skill 介绍

**Habit Tracker** 是一款轻量级的习惯追踪系统，帮助用户养成和管理日常习惯。

#### 核心功能
- ✅ 添加和管理多个习惯（喝水、阅读、运动等）
- 📝 每日打卡记录
- 📊 统计数据：连续天数、完成率
- 📈 可视化报表：周/月统计表格
- 🔥 GitHub 风格连续打卡热力图
- 💾 JSON 数据持久化 + Markdown 导出

#### 技术亮点
- Python 面向对象设计
- JSON 数据存储
- Markdown 格式报告生成
- 连续打卡天数自动计算
- 周/月完成率统计

### 2️⃣ 使用场景

| 场景 | 示例习惯 |
|------|----------|
| 💧 健康饮水 | 每天喝8杯水 |
| 📚 每日阅读 | 每天阅读30分钟 |
| 🏃 运动健身 | 每天锻炼 |
| 😴 早睡早起 | 23点前睡觉 |
| 💊 健康管理 | 按时吃药、吃维生素 |
| ✍️ 写作日更 | 每天写500字 |

### 3️⃣ 使用 SOLO 的创作过程

```
Step 1: 需求分析
├── 痛点：想养成好习惯，但总是半途而废
├── 目标：简单记录、清晰展示、坚持激励
└── 方案：命令行习惯追踪工具

Step 2: 数据结构设计
├── habits[] - 习惯列表（id, name, target, unit, frequency）
├── records[] - 打卡记录（habit_id, date, value, completed）
└── JSON 文件持久化存储

Step 3: 核心功能实现
├── add_habit() - 添加新习惯
├── check_in() - 每日打卡
├── get_streak() - 计算连续天数
├── get_weekly_report() - 周报统计
└── generate_markdown_report() - Markdown 输出

Step 4: 封装为 Skill
├── 定义 trigger keywords
├── 编写 Python 类模板
├── 提供使用示例
└── 设计 Markdown 报告格式
```

### 4️⃣ 调用步骤

#### 方式一：直接对话
```
用户：我想养成每天喝8杯水的习惯
SOLO：调用 habit-tracker skill
     - 创建 "喝水" 习惯，target=8, unit="杯"
     - 提供每日打卡方法

用户：今天喝了6杯水，打卡
SOLO：tracker.check_in("habit_001", value=6)

用户：生成周报
SOLO：tracker.generate_markdown_report()
```

#### 方式二：Python 代码调用
```python
from habit_tracker import HabitTracker

# 初始化
tracker = HabitTracker()

# 添加习惯
tracker.add_habit("喝水量", target=8, unit="杯", frequency="daily")
tracker.add_habit("阅读", target=30, unit="分钟", frequency="daily")

# 每日打卡
tracker.check_in("habit_001", value=8, note="今天喝水达标了！")
tracker.check_in("habit_002", value=45, note="读了半本书")

# 查看连续打卡天数
print(f"喝水连续: {tracker.get_streak('habit_001')} 天")

# 生成周报
print(tracker.generate_markdown_report())
```

### 5️⃣ 效果展示

**周报 Markdown 输出**：
```markdown
# 📅 Habit Report (2025-05-26)

## 🔥 Streaks
- 💧 喝水量: 12 days 🔥
- 📚 阅读: 5 days
- 🏃 运动: 3 days

## 📊 Completion Rates
| Habit | Completed | Target | Rate |
|-------|-----------|--------|------|
| 💧 喝水量 | 7 | 7 | 100.0% |
| 📚 阅读 | 5 | 7 | 71.4% |
| 🏃 运动 | 3 | 7 | 42.9% |

## 💡 Insights
- Best habit: 喝水量 (100% completion)
- Needs improvement: 运动
- Total check-ins this week: 15
```

### 6️⃣ Skill 链接

> 📍 安装路径：`.trae/skills/habit-tracker/SKILL.md`

---

## 🎁 创作福利说明

本次投稿符合活动要求：

| 要求 | 状态 | 说明 |
|------|------|------|
| ✅ 创作时间 | ✓ | 05.25 20:00 - 05.29 在规定时间内 |
| ✅ 原创作品 | ✓ | 使用 SOLO 独立创作，非抄袭搬运 |
| ✅ 完整说明 | ✓ | 包含：介绍、场景、过程、步骤、效果 |
| ✅ Skill 格式 | ✓ | 符合 `.trae/skills/<name>/SKILL.md` 结构 |

---

## 📂 文件结构

```
.trae/skills/
├── wechat_article_scraper/
│   └── SKILL.md          # 微信公众号文章抓取工具
└── habit-tracker/
    └── SKILL.md          # 习惯追踪打卡系统
```

---

## 🚀 安装使用

在 TRAE 中安装 Skill：

1. 打开 TRAE 设置
2. 进入 Skills 管理
3. 将 `SKILL.md` 文件内容复制到对应路径
4. 重启 TRAE 即可使用

---

## 💡 创作心得

使用 SOLO 创作这两个 Skill 的过程中，我深刻体验到了 AI 辅助编程的便捷：

1. **快速原型**：SOLO 能够快速生成代码框架，减少重复工作
2. **智能补全**：提供完整的类设计和函数实现
3. **文档完善**：自动生成使用说明和示例代码
4. **格式规范**：输出的 Markdown 结构清晰，便于阅读

这两个 Skill 都是从日常痛点出发，旨在解决实际问题：
- 📰 WeChat Scraper 解决"无法方便地保存公众号文章"的痛点
- 📅 Habit Tracker 解决"习惯难以坚持"的痛点

希望这些 Skill 能够帮助更多人提升效率、养成好习惯！

---

*© 2025 fupengyu1 - TRAE Skill 创作赛投稿作品*
