---
name: "habit-tracker"
description: "Track daily habits, generate weekly/monthly statistics with visual charts, and export progress reports. Invoke when user wants to build habits, track routines, or visualize consistency streaks."
---

# 📅 Habit Tracker

## 🎯 Overview
A lightweight habit tracking system that helps users build and maintain daily routines. Track multiple habits, visualize progress with charts, and generate shareable reports.

## 💡 When to Use
- Building new habits (drinking water, reading, exercise)
- Tracking daily routines and consistency
- Generating weekly/monthly progress reports
- Visualizing streaks and completion rates

## 🎯 Use Cases
- **Daily Routines**: Water intake, reading, meditation, exercise
- **Health Habits**: Sleep schedule, medication, vitamins
- **Productivity**: Deep work, learning, journaling
- **Social**: Calling family, meeting friends

## 🚀 Capabilities

### 1️⃣ Habit Management
- Add/remove habits with custom names
- Set frequency (daily, weekdays, weekends, custom)
- Configure target counts (e.g., drink 8 glasses of water)

### 2️⃣ Daily Check-in
- Mark habits as complete
- Partial completion support
- Skip days with reason logging

### 3️⃣ Statistics & Visualization
- **Streak Counter**: Current and longest streak
- **Completion Rate**: Daily/weekly/monthly percentages
- **Trend Charts**: Line/bar charts showing progress over time
- **Heatmap Calendar**: GitHub-style contribution graph

### 4️⃣ Export & Share
- Generate weekly/monthly reports
- Export to Markdown for sharing
- JSON backup for data portability

## 🛠️ Implementation

### Data Structure
```json
{
  "habits": [
    {
      "id": "habit_001",
      "name": "Drink Water",
      "target": 8,
      "unit": "glasses",
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
      "note": ""
    }
  ]
}
```

### Python Class Template
```python
import json
import os
from datetime import datetime, timedelta

class HabitTracker:
    def __init__(self, data_file="habits.json"):
        self.data_file = data_file
        self.data = {"habits": [], "records": []}
        self.load()
    
    def load(self):
        if os.path.exists(self.data_file):
            with open(self.data_file, 'r', encoding='utf-8') as f:
                self.data = json.load(f)
    
    def save(self):
        with open(self.data_file, 'w', encoding='utf-8') as f:
            json.dump(self.data, f, ensure_ascii=False, indent=2)
    
    def add_habit(self, name, target=1, unit="times", frequency="daily"):
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
        target = next((h["target"] for h in self.data["habits"] if h["id"] == habit_id), 1)
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
        records = [r for r in self.data["records"] if r["habit_id"] == habit_id and r["completed"]]
        if not records:
            return 0
        
        dates = sorted(set(r["date"] for r in records), reverse=True)
        streak = 0
        today = datetime.now().date()
        
        for i, date_str in enumerate(dates):
            date = datetime.strptime(date_str, "%Y-%m-%d").date()
            expected = today - timedelta(days=i)
            if date == expected:
                streak += 1
            else:
                break
        return streak
    
    def get_weekly_report(self):
        end_date = datetime.now().date()
        start_date = end_date - timedelta(days=6)
        
        report = {}
        for habit in self.data["habits"]:
            records = [r for r in self.data["records"] 
                      if r["habit_id"] == habit["id"] 
                      and start_date <= datetime.strptime(r["date"], "%Y-%m-%d").date() <= end_date]
            completed_days = len([r for r in records if r["completed"]])
            report[habit["name"]] = {
                "target_days": 7,
                "completed_days": completed_days,
                "rate": f"{completed_days / 7 * 100:.1f}%"
            }
        return report
    
    def generate_markdown_report(self):
        report = self.get_weekly_report()
        today = datetime.now().strftime("%Y-%m-%d")
        
        lines = [f"# 📅 Habit Report ({today})\n"]
        lines.append("\n## 🔥 Streaks")
        
        for habit in self.data["habits"]:
            streak = self.get_streak(habit["id"])
            emoji = "🔥" if streak >= 7 else ""
            lines.append(f"- {habit['name']}: {streak} days {emoji}")
        
        lines.append("\n## 📊 Completion Rates")
        lines.append("| Habit | Completed | Target | Rate |")
        lines.append("|-------|-----------|--------|------|")
        
        for name, stats in report.items():
            lines.append(f"| {name} | {stats['completed_days']} | {stats['target_days']} | {stats['rate']} |")
        
        return "\n".join(lines)
```

## 📊 Usage Examples

### Create a New Habit
```python
tracker = HabitTracker()
tracker.add_habit("Drink Water", target=8, unit="glasses", frequency="daily")
tracker.add_habit("Read Books", target=30, unit="minutes", frequency="daily")
```

### Daily Check-in
```python
tracker.check_in("habit_001", value=8, note="Met my goal today!")
tracker.check_in("habit_002", value=45, note="Finished Chapter 3")
```

### View Weekly Report
```python
print(tracker.generate_markdown_report())
```

## 🎨 Example Output

```markdown
# 📅 Habit Report (2025-05-26)

## 🔥 Streaks
- Drink Water: 12 days 🔥
- Read Books: 5 days
- Exercise: 3 days

## 📊 Completion Rates
| Habit | Completed | Target | Rate |
|-------|-----------|--------|------|
| Drink Water | 7 | 7 | 100.0% |
| Read Books | 5 | 7 | 71.4% |
| Exercise | 3 | 7 | 42.9% |

## 💡 Insights
- Best habit: Drink Water (100% completion)
- Needs improvement: Exercise
- Total check-ins this week: 15
```

## ⚡ Quick Start
1. Initialize tracker: `tracker = HabitTracker()`
2. Add habits: `tracker.add_habit("Habit Name", target=X, unit="units")`
3. Daily check-in: `tracker.check_in("habit_001", value=X)`
4. Get report: `tracker.generate_markdown_report()`

## 🚀 Trigger Keywords
- "习惯打卡"
- "习惯追踪"
- "habit tracker"
- "每日打卡"
- "坚持了多少天"
- "生成周报"
