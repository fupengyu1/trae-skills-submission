---
name: "pet-care-assistant"
description: "Provides comprehensive pet care advice including feeding schedules, health management, training tips, and vaccination reminders. Invoke when user has pet care questions, needs feeding plans, or wants to track pet health records."
---

# 🐾 Pet Care Assistant

## 🎯 Overview
A comprehensive pet care companion that helps manage all aspects of pet ownership. From feeding schedules and nutrition advice to health tracking and training tips. Supports dogs, cats, birds, fish, hamsters, and more.

## 💡 When to Use
- Get feeding and nutrition advice for pets
- Track vaccinations and health records
- Get training tips and behavior guidance
- Set care reminders and schedules
- Emergency first aid information

## ⚔️ Execution Rules
1. **Pet Profile**: Create and maintain individual pet profiles
2. **Care Database**: Access breed-specific information
3. **Schedule Management**: Track vaccinations, vet visits, medications
4. **Health Logging**: Record weight, symptoms, medications
5. **Expert Advice**: Generate personalized care recommendations

## 🛠️ Usage

### Step 1: Provide Pet Information
User specifies pet type, breed, age, and specific concerns

### Step 2: Get Care Plan
```python
class PetCareAssistant:
    def __init__(self):
        self.pets = []
        self.care_db = load_pet_database()
    
    def add_pet(self, name, species, breed, age, weight):
        """Register a new pet"""
        pet = {
            "id": f"pet_{len(self.pets) + 1:03d}",
            "name": name,
            "species": species,  # dog, cat, bird, hamster, fish...
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
        """Generate feeding schedule and nutrition guide"""
        pet = self.get_pet(pet_id)
        species = pet["species"]
        weight = pet["weight"]
        
        # Calculate daily food needs
        daily_amount = calculate_daily_food(species, weight)
        
        # Get feeding schedule
        schedule = self.care_db[species]["feeding_schedule"]
        
        return {
            "daily_amount": daily_amount,
            "schedule": schedule,
            "nutrition_tips": self.care_db[species]["nutrition_tips"]
        }
    
    def add_vaccination(self, pet_id, vaccine, date):
        """Record vaccination"""
        pet = self.get_pet(pet_id)
        pet["vaccinations"].append({
            "vaccine": vaccine,
            "date": date,
            "next_due": calculate_next_due(date, vaccine)
        })
    
    def get_health_reminders(self, pet_id):
        """Generate upcoming health reminders"""
        pet = self.get_pet(pet_id)
        reminders = []
        
        # Check vaccinations due
        for vac in pet["vaccinations"]:
            if vac["next_due"]:
                reminders.append(f"Vaccination: {vac['vaccine']} due on {vac['next_due']}")
        
        # Add routine care reminders
        reminders.extend([
            "Monthly flea/tick prevention",
            "Quarterly deworming",
            "Annual health checkup"
        ])
        
        return reminders
    
    def generate_care_report(self, pet_id):
        """Generate comprehensive care report"""
        pet = self.get_pet(pet_id)
        feeding = self.get_feeding_guide(pet_id)
        reminders = self.get_health_reminders(pet_id)
        
        return {
            "pet_info": pet,
            "feeding_guide": feeding,
            "health_reminders": reminders,
            "training_tips": self.care_db[pet["species"]]["training_tips"]
        }

# Example usage
assistant = PetCareAssistant()
assistant.add_pet("球球", "dog", "金毛", age=2, weight=30)
assistant.add_vaccination("pet_001", "狂犬疫苗", "2025-03-15")

report = assistant.generate_care_report("pet_001")
print(report)
```

### Step 3: Get Care Report
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

## 🎯 Supported Features
- ✅ Multi-pet profile management
- ✅ Species and breed-specific advice
- ✅ Feeding schedule generator
- ✅ Vaccination tracking
- ✅ Health record logging
- ✅ Medication reminders
- ✅ Training tips and behavior guidance
- ✅ Emergency first aid info

## ⚠️ Limitations
- Not a substitute for veterinary care
- Nutritional values are estimates
- Breed-specific data coverage varies

## 🚀 Trigger Keywords
- "宠物喂养"
- "怎么养猫/狗"
- "宠物健康"
- "pet care"
- "dog training"
- "cat food"
- "宠物打疫苗"
