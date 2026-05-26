# 🍳 Recipe Nutritionist

> 智能营养分析工具 - 计算热量、营养成分、健康建议

## 📖 简介

**Recipe Nutritionist** 是一款专门用于分析食谱营养成分的 TRAE Skill。输入食材或菜谱，自动计算卡路里、蛋白质、碳水、脂肪等营养成分，并生成个性化的健康饮食建议。

## ✨ 核心功能

| 功能 | 说明 |
|------|------|
| 🔢 热量计算 | 自动计算菜品总热量和单位热量 |
| 📊 营养成分分析 | 蛋白质、碳水、脂肪、纤维素等 |
| ⚖️ 每日摄入占比 | 对比官方推荐摄入量 |
| 💡 健康建议 | 根据饮食目标给出优化建议 |
| 🍽️ 饮食追踪 | 记录每日饮食，计算营养摄入 |

## 🎯 使用场景

| 场景 | 示例 |
|------|------|
| 🏋️ 健身减脂 | 计算每餐热量，控制摄入 |
| 🩺 健康管理 | 糖尿病、高血压患者饮食管理 |
| 👶 儿童营养 | 确保孩子饮食均衡 |
| 🤰 孕期饮食 | 科学搭配孕期营养 |

## 🚀 快速开始

### 方式一：直接对话（推荐）

```
用户：帮我分析这个食谱的热量
      鸡胸肉200g + 西兰花100g + 糙米150g

SOLO：调用 recipe-nutritionist skill
      生成营养分析报告
```

### 方式二：Python 代码调用

```python
def analyze_nutrition(ingredients):
    """分析食材营养成分"""
    nutrition_data = {
        "total_calories": 0,
        "macros": {"protein": 0, "carbs": 0, "fat": 0},
        "fiber": 0,
        "sodium": 0
    }
    
    for item in ingredients:
        # 查找每100g营养数据
        per_100g = get_nutrition_data(item["name"])
        # 按实际用量计算
        grams = convert_to_grams(item["amount"], item["unit"])
        multiplier = grams / 100
        
        nutrition_data["total_calories"] += per_100g["calories"] * multiplier
        nutrition_data["macros"]["protein"] += per_100g["protein"] * multiplier
        nutrition_data["macros"]["carbs"] += per_100g["carbs"] * multiplier
        nutrition_data["macros"]["fat"] += per_100g["fat"] * multiplier
    
    return nutrition_data

# 使用示例
ingredients = [
    {"name": "鸡胸肉", "amount": 200, "unit": "g"},
    {"name": "西兰花", "amount": 100, "unit": "g"},
    {"name": "糙米", "amount": 150, "unit": "g"}
]

result = analyze_nutrition(ingredients)
print(f"总热量: {result['total_calories']} kcal")
print(f"蛋白质: {result['macros']['protein']}g")
```

## 📊 输出示例

```markdown
# 🍽️ 营养分析报告

## 📊 营养成分（每份）
| 营养素 | 含量 | 每日推荐% |
|--------|------|----------|
| 热量 | 450 kcal | 22% |
| 蛋白质 | 35g | 70% |
| 碳水 | 45g | 15% |
| 脂肪 | 12g | 15% |
| 纤维素 | 6g | 24% |

## ⚠️ 健康分析
- ✅ 高蛋白 - 有利于肌肉增长
- ✅ 低钠 - 保护心血管
- ⚡ 适量碳水 - 适合运动人群

## 💡 优化建议
- 可添加牛油果或橄榄油，补充健康脂肪
- 建议增加绿叶蔬菜，提升维生素摄入
```

## 🗂️ 营养数据库（部分）

| 食材 | 热量(kcal/100g) | 蛋白质(g) | 碳水(g) | 脂肪(g) |
|------|-----------------|-----------|---------|---------|
| 鸡胸肉 | 165 | 31 | 0 | 3.6 |
| 西兰花 | 34 | 2.8 | 7 | 0.4 |
| 糙米 | 111 | 2.6 | 23 | 0.9 |
| 三文鱼 | 208 | 20 | 0 | 13 |
| 鸡蛋 | 155 | 13 | 1.1 | 11 |

## 📈 功能架构

```
┌─────────────────────────────────────────────┐
│           Recipe Nutritionist               │
├─────────────────────────────────────────────┤
│  食材解析                                   │
│  ├── parse_recipe()     解析食谱文本        │
│  ├── convert_units()     单位换算           │
│  └── extract_ingredients() 提取食材列表      │
├─────────────────────────────────────────────┤
│  营养计算                                   │
│  ├── get_nutrition_data() 查询营养数据库     │
│  ├── calculate_total()   计算总量           │
│  └── calculate_dv()      计算每日占比        │
├─────────────────────────────────────────────┤
│  健康分析                                   │
│  ├── analyze_health()   健康评估            │
│  ├── check_diet_goals() 饮食目标对比        │
│  └── generate_tips()    生成建议            │
├─────────────────────────────────────────────┤
│  报告生成                                   │
│  ├── markdown_report()  Markdown报告        │
│  └── daily_summary()    日摄入汇总         │
└─────────────────────────────────────────────┘
```

## 🔗 Skill 链接

**GitHub 完整地址**：
- Skill 源码：https://github.com/fupengyu1/trae-skills-submission/blob/main/.trae/skills/recipe-nutritionist/SKILL.md
- 本地路径：`.trae/skills/recipe-nutritionist/SKILL.md`

## 📁 文件结构

```
recipe-nutritionist/
├── README.md      # 本文件
└── SKILL.md      # Skill 核心定义
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📜 许可证

MIT License

---

*使用 SOLO + TRAE 创作于 2025-05-26*
