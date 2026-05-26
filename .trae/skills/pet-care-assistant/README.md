# 🐾 Pet Care Assistant

> 全方位宠物养护顾问 - 喂养指南、健康追踪、训练建议

## 📖 简介

**Pet Care Assistant** 是一款全方位的宠物养护助手。支持猫、狗、鸟类、仓鼠、鱼等多种宠物，提供喂养计划、健康管理、疫苗追踪、训练指导等一站式服务。

## ✨ 核心功能

| 功能 | 说明 |
|------|------|
| 🐕🐱 多宠管理 | 同时管理多只不同种类的宠物 |
| 🍖 喂养指南 | 根据品种、年龄、体重定制喂养计划 |
| 💉 疫苗追踪 | 记录疫苗接种，自动提醒下次时间 |
| 📊 健康日志 | 记录体重、症状、用药情况 |
| 🎓 训练建议 | 提供行为训练技巧和方法 |
| ⏰ 护理提醒 | 设置定期护理任务提醒 |

## 🎯 使用场景

| 场景 | 示例 |
|------|------|
| 🐶 新手养狗 | 不知道该怎么喂养、训练 |
| 🐱 猫咪养护 | 猫粮选择、健康问题 |
| 🐹 异宠饲养 | 仓鼠、兔子、龙猫等 |
| 💊 健康管理 | 疫苗时间、体重监控 |
| 🏥 就医准备 | 整理宠物健康档案 |

## 🚀 快速开始

### 方式一：直接对话（推荐）

```
用户：我刚养了一只2个月大的金毛，该怎么喂？

SOLO：调用 pet-care-assistant skill
      - 创建宠物档案
      - 提供喂养指南
      - 设置疫苗提醒
```

### 方式二：Python 代码调用

```python
class PetCareAssistant:
    def __init__(self):
        self.pets = []
        self.care_db = load_pet_database()
    
    def add_pet(self, name, species, breed, age, weight):
        """注册新宠物"""
        pet = {
            "id": f"pet_{len(self.pets) + 1:03d}",
            "name": name,
            "species": species,
            "breed": breed,
            "age": age,
            "weight": weight,
            "vaccinations": [],
            "health_records": [],
            "feeding_schedule": {}
        }
        self.pets.append(pet)
        return pet["id"]
    
    def get_feeding_guide(self, pet_id):
        """生成喂养指南"""
        pet = self.get_pet(pet_id)
        species = pet["species"]
        weight = pet["weight"]
        
        daily_amount = calculate_daily_food(species, weight)
        schedule = self.care_db[species]["feeding_schedule"]
        
        return {
            "daily_amount": daily_amount,
            "schedule": schedule,
            "nutrition_tips": self.care_db[species]["nutrition_tips"]
        }
    
    def add_vaccination(self, pet_id, vaccine, date):
        """记录疫苗接种"""
        pet = self.get_pet(pet_id)
        pet["vaccinations"].append({
            "vaccine": vaccine,
            "date": date,
            "next_due": calculate_next_due(date, vaccine)
        })
    
    def get_health_reminders(self, pet_id):
        """生成健康提醒"""
        pet = self.get_pet(pet_id)
        reminders = []
        
        for vac in pet["vaccinations"]:
            if vac["next_due"]:
                reminders.append(f"{vac['vaccine']} 到期: {vac['next_due']}")
        
        reminders.extend([
            "每月1日：体外驱虫",
            "每季度：体内驱虫",
            "每年：年度体检"
        ])
        
        return reminders

# 使用示例
assistant = PetCareAssistant()
assistant.add_pet("球球", "dog", "金毛", age=2, weight=30)
assistant.add_vaccination("pet_001", "狂犬疫苗", "2025-03-15")

report = assistant.generate_care_report("pet_001")
```

## 📊 输出示例

```markdown
# 🐾 宠物健康报告 - 球球

## 📋 基本信息
| 项目 | 内容 |
|------|------|
| 名字 | 球球 |
| 种类 | 狗 |
| 品种 | 金毛 |
| 年龄 | 2岁 |
| 体重 | 30kg |

## 🍖 喂养指南
- **每日食量**: 300-400g 狗粮
- **喂食时间**: 早8点、晚6点
- **零食**: 控制在总热量的10%以内

### 💡 营养建议
- 金毛容易发胖，注意控制食量
- 补充软骨素，保护关节
- 每周2-3个蛋黄，美毛亮毛

## 💉 疫苗记录
| 疫苗 | 接种日期 | 下次接种 |
|------|----------|----------|
| 狂犬疫苗 | 2025-03-15 | 2026-03-15 |
| 犬瘟热 | 2024-12-01 | 2025-12-01 |

## 📅 待办提醒
- ⏰ 6月1日：狂犬疫苗加强针
- ⏰ 每月1日：体外驱虫
- ⏰ 每季度：体内驱虫

## 🎓 训练建议
- 金毛服从性强，建议从基础指令开始
- 奖励训练法效果最好
- 每日遛狗不少于1小时
```

## 🗂️ 宠物数据库（部分）

### 🐕 狗狗

| 项目 | 内容 |
|------|------|
| 每日食量 | 体重(kg) × 30-40 kcal |
| 喂食次数 | 幼犬3次/天，成犬2次/天 |
| 寿命 | 10-15年 |
| 疫苗 | 狂犬、犬瘟热、犬细小、犬腺病毒 |

### 🐱 猫咪

| 项目 | 内容 |
|------|------|
| 每日食量 | 体重(kg) × 40-50 kcal |
| 喂食次数 | 自由采食或2次/天 |
| 寿命 | 12-18年 |
| 疫苗 | 猫三联、狂犬 |

## 📈 功能架构

```
┌─────────────────────────────────────────────┐
│           Pet Care Assistant                │
├─────────────────────────────────────────────┤
│  宠物档案                                   │
│  ├── add_pet()          添加宠物            │
│  ├── update_pet()       更新信息            │
│  └── get_pet()          获取档案            │
├─────────────────────────────────────────────┤
│  喂养管理                                   │
│  ├── get_feeding_guide() 喂养指南           │
│  ├── calculate_nutrition() 营养计算         │
│  └── suggest_food()     食物推荐            │
├─────────────────────────────────────────────┤
│  健康追踪                                   │
│  ├── add_vaccination()  疫苗记录           │
│  ├── add_health_record() 健康日志          │
│  └── get_health_reminders() 提醒           │
├─────────────────────────────────────────────┤
│  训练指导                                   │
│  ├── get_training_tips()  训练技巧          │
│  ├── get_behavior_guide() 行为指南         │
│  └── generate_report()  生成报告           │
└─────────────────────────────────────────────┘
```

## 🔗 Skill 链接

**GitHub 完整地址**：
- Skill 源码：https://github.com/fupengyu1/trae-skills-submission/blob/main/.trae/skills/pet-care-assistant/SKILL.md
- 本地路径：`.trae/skills/pet-care-assistant/SKILL.md`

## 📁 文件结构

```
pet-care-assistant/
├── README.md      # 本文件
└── SKILL.md      # Skill 核心定义
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📜 许可证

MIT License

---

*使用 SOLO + TRAE 创作于 2025-05-26*
