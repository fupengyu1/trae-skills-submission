# 📅 Habit Tracker

> 轻量级习惯追踪系统 - 打卡、统计、可视化报告

## 📖 简介

**Habit Tracker** 是一款帮助用户养成和管理日常习惯的 TRAE Skill。简洁的数据结构、清晰的统计报表、激励人心的连续打卡机制，让好习惯坚持不再困难。

## ✨ 核心功能

| 功能 | 说明 |
|------|------|
| ✅ 习惯管理 | 添加、删除、修改习惯 |
| 📝 每日打卡 | 记录完成情况，支持备注 |
| 🔥 连续天数 | 自动计算当前和最长连续打卡天数 |
| 📊 统计报表 | 周/月完成率统计 |
| 📈 可视化 | Markdown 格式的表格报告 |
| 💾 数据持久化 | JSON 文件存储 |

## 🎯 使用场景

| 场景 | 示例习惯 |
|------|----------|
| 💧 健康饮水 | 每天喝 8 杯水 |
| 📚 每日阅读 | 每天阅读 30 分钟 |
| 🏃 运动健身 | 每天锻炼 |
| 😴 早睡早起 | 23 点前睡觉 |
| 💊 健康管理 | 按时吃药、吃维生素 |
| ✍️ 写作日更 | 每天写 500 字 |
| 🧘 冥想放松 | 每天冥想 10 分钟 |

## 🚀 快速开始

### 方式一：直接对话（推荐）

```
用户：我想养成每天喝 8 杯水的习惯

SOLO：调用 habit-tracker skill
      - 创建 "喝水量" 习惯，target=8, unit="杯"
      - 提供每日打卡方法

用户：今天喝了 6 杯水，打卡

SOLO：tracker.check_in("habit_001", value=6)

用户：生成周报

SOLO：tracker.generate_markdown_report()
```

### 方式二：Python 代码调用

```python
from datetime import datetime
import json

class HabitTracker:
    def __init__(self, data_file="habits.json"):
        self.data_file = data_file
        self.data = {"habits": [], "records": []}
        self.load()
    
    def load(self):
        try:
            with open(self.data_file, 'r', encoding='utf-8') as f:
                self.data = json.load(f)
        except FileNotFoundError:
            pass
    
    def save(self):
        with open(self.data_file, 'w', encoding='utf-8') as f:
            json.dump(self.data, f, ensure_ascii=False, indent=2)
    
    def add_habit(self, name, target=1, unit="次", frequency="daily"):
        habit = {
            "id": f"habit_{len(self.data['habits']) + 1:03d}",
            "name": name,
            "target": target,
            "unit": unit,
            "frequency": frequency,
            "created_at": datetime.now().strftime("%Y-%m-%d")
        }
        self.data["habits"].append(habit)
        self.save()
        return habit["id"]
    
    def check_in(self, habit_id, value=1, note=""):
        target = next((h["target"] for h in self.data["habits"] 
                      if h["id"] == habit_id), 1)
        record = {
            "habit_id": habit_id,
            "date": datetime.now().strftime("%Y-%m-%d"),
            "completed": value >= target,
            "value": value,
            "note": note
        }
        self.data["records"].append(record)
        self.save()
        return record
    
    def get_streak(self, habit_id):
        records = [r for r in self.data["records"] 
                  if r["habit_id"] == habit_id and r["completed"]]
        if not records:
            return 0
        
        from datetime import timedelta
        dates = sorted(set(r["date"] for r in records), reverse=True)
        streak = 0
        today = datetime.now().date()
        
        for i, date_str in enumerate(dates):
            date = datetime.strptime(date_str, "%Y-%m-%d").date()
            if date == today - timedelta(days=i):
                streak += 1
            else:
                break
        return streak
    
    def generate_markdown_report(self):
        from datetime import timedelta
        end_date = datetime.now().date()
        start_date = end_date - timedelta(days=6)
        
        lines = [f"# 📅 Habit Report ({end_date.strftime('%Y-%m-%d')})\n"]
        lines.append("\n## 🔥 Streaks")
        
        for habit in self.data["habits"]:
            streak = self.get_streak(habit["id"])
            emoji = "🔥" if streak >= 7 else ""
            lines.append(f"- {habit['name']}: {streak} days {emoji}")
        
        lines.append("\n## 📊 Completion Rates")
        lines.append("| Habit | Completed | Target | Rate |")
        lines.append("|-------|-----------|--------|------|")
        
        for habit in self.data["habits"]:
            records = [r for r in self.data["records"] 
                      if r["habit_id"] == habit["id"]
                      and start_date <= datetime.strptime(r["date"], "%Y-%m-%d").date() <= end_date]
            completed = len([r for r in records if r["completed"]])
            rate = completed / 7 * 100
            lines.append(f"| {habit['name']} | {completed} | 7 | {rate:.1f}% |")
        
        return "\n".join(lines)

# 使用示例
tracker = HabitTracker()
tracker.add_habit("喝水量", target=8, unit="杯")
tracker.add_habit("阅读", target=30, unit="分钟")

tracker.check_in("habit_001", value=8, note="今天达标了！")
tracker.check_in("habit_002", value=45, note="读了半本书")

print(tracker.generate_markdown_report())
```

## 📊 输出示例

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

## 🗂️ 数据结构

```json
{
  "habits": [
    {
      "id": "habit_001",
      "name": "喝水量",
      "target": 8,
      "unit": "杯",
      "frequency": "daily",
      "created_at": "2025-05-26"
    }
  ],
  "records": [
    {
      "habit_id": "habit_001",
      "date": "2025-05-26",
      "completed": true,
      "value": 8,
      "note": "今天达标了！"
    }
  ]
}
```

## 📈 功能架构

```
┌─────────────────────────────────────────────┐
│              HabitTracker                    │
├─────────────────────────────────────────────┤
│  习惯管理                                    │
│  ├── add_habit()     添加新习惯             │
│  ├── remove_habit()  删除习惯               │
│  └── list_habits()   列出所有习惯            │
├─────────────────────────────────────────────┤
│  打卡记录                                    │
│  ├── check_in()      每日打卡                │
│  └── get_history()   查看历史记录            │
├─────────────────────────────────────────────┤
│  数据分析                                    │
│  ├── get_streak()     计算连续天数           │
│  ├── get_weekly_report()  周报统计           │
│  └── get_monthly_report() 月报统计           │
├─────────────────────────────────────────────┤
│  导出分享                                    │
│  ├── generate_markdown_report()  Markdown    │
│  └── export_json()    JSON 备份             │
└─────────────────────────────────────────────┘
```

## 📁 文件结构

```
habit-tracker/
├── README.md      # 本文件
└── SKILL.md      # Skill 核心定义
```

## 💡 使用技巧

1. **早起打卡**：设置固定时间提醒，养成习惯
2. **目标适中**：刚开始目标不要太高，循序渐进
3. **记录备注**：打卡时写点心得，更有成就感
4. **周报复盘**：每周生成报告，分析改进

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📜 许可证

MIT License

---

*使用 SOLO + TRAE 创作于 2025-05-26*
