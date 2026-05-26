# ✈️ Travel Itinerary Planner

> 智能旅行规划助手 - 制定行程、推荐酒店、规划路线

## 📖 简介

**Travel Itinerary Planner** 是一款智能旅行规划助手。输入目的地、日期、预算和偏好，自动生成详细的每日行程安排、酒店推荐、餐饮建议、交通方案，以及打包清单。

## ✨ 核心功能

| 功能 | 说明 |
|------|------|
| 📅 每日行程 | 按天规划景点游览顺序 |
| 🏨 酒店推荐 | 根据预算推荐住宿 |
| 🍜 美食指南 | 当地特色餐厅推荐 |
| 🚄 交通方案 | 景点间接驳路线 |
| 💰 预算估算 | 预估每日花费 |
| 📦 打包清单 | 生成出行准备列表 |

## 🎯 使用场景

| 场景 | 示例 |
|------|------|
| 🏖️ 度假旅行 | 三亚5日休闲游 |
| 🏙️ 城市探索 | 上海周末打卡游 |
| 🎒 户外徒步 | 川西高原探险 |
| 👨‍👩‍👧 亲子出游 | 迪士尼2日游 |
| 💼 出差商务 | 北京3日会议行 |

## 🚀 快速开始

### 方式一：直接对话（推荐）

```
用户：帮我规划一个杭州3日游，预算中等，喜欢慢节奏

SOLO：调用 travel-itinerary skill
      生成每日详细行程和推荐
```

### 方式二：Python 代码调用

```python
def generate_itinerary(destination, days, budget="medium", style="balanced"):
    """生成旅行行程"""
    itinerary = {
        "destination": destination,
        "duration": days,
        "budget": budget,
        "style": style,
        "daily_plans": [],
        "hotels": [],
        "restaurants": [],
        "tips": []
    }
    
    # 目的地研究
    info = get_destination_info(destination)
    
    # 生成每日计划
    for day in range(1, days + 1):
        daily_plan = create_daily_plan(
            destination=destination,
            day=day,
            style=style,
            weather=get_weather_forecast(destination, day)
        )
        itinerary["daily_plans"].append(daily_plan)
    
    # 酒店推荐
    itinerary["hotels"] = get_hotel_recommendations(destination, budget)
    
    # 餐厅推荐
    itinerary["restaurants"] = get_restaurant_recommendations(destination)
    
    # 当地贴士
    itinerary["tips"] = get_local_tips(destination)
    
    return itinerary

# 使用示例
result = generate_itinerary(
    destination="杭州",
    days=3,
    budget="medium",
    style="balanced"
)

for day_plan in result["daily_plans"]:
    print(f"\n📅 {day_plan['title']}")
    for item in day_plan["schedule"]:
        print(f"  {item['time']} - {item['activity']}")
```

## 📊 输出示例

```markdown
# ✈️ 杭州 3日游行程

## 📅 Day 1: 西湖精华
**主题**: 经典打卡 + 历史文化

### 🕐 上午
- 08:00 酒店早餐
- 09:00 西湖断桥残雪
- 10:30 白堤散步
- 12:00 知味观午餐（杭帮菜）

### 🕑 下午
- 14:00 雷峰塔登高望远
- 16:00 苏堤春晓
- 18:00 西湖音乐喷泉

### 🕘 晚上
- 19:30 河坊街夜市
- 住宿：杭州西湖 JW 万豪酒店

## 🏨 酒店推荐
| 酒店 | 星级 | 价格/晚 | 位置 |
|------|------|---------|------|
| 西子四季 | ⭐⭐⭐⭐ | ¥600 | 西湖边 |
| 开元名都 | ⭐⭐⭐⭐⭐ | ¥900 | 市中心 |

## 🍜 美食推荐
- 知味观（杭帮菜经典）
- 楼外楼（西湖醋鱼）
- 外婆家（性价比高）

## 💡 当地贴士
- 西湖周边停车困难，建议地铁+步行
- 周末人流量大，建议早起出行
```

## 🗺️ 行程规划逻辑

```
┌─────────────────────────────────────────────┐
│          Travel Itinerary Planner           │
├─────────────────────────────────────────────┤
│  目的地分析                                 │
│  ├── get_destination_info()  目的地信息     │
│  ├── get_attractions()       景点列表        │
│  └── get_seasonal_tips()     季节建议        │
├─────────────────────────────────────────────┤
│  行程规划                                   │
│  ├── optimize_route()      路线优化         │
│  ├── create_daily_plan()   每日计划         │
│  └── estimate_time()       时间估算         │
├─────────────────────────────────────────────┤
│  资源推荐                                   │
│  ├── get_hotel_recommendations() 酒店       │
│  ├── get_restaurant_recommendations() 餐厅  │
│  └── get_transport_options()  交通方案       │
├─────────────────────────────────────────────┤
│  预算管理                                   │
│  ├── estimate_budget()     预算估算         │
│  └── generate_checklist()  打包清单         │
└─────────────────────────────────────────────┘
```

## 🔗 Skill 链接

**GitHub 完整地址**：
- Skill 源码：https://github.com/fupengyu1/trae-skills-submission/blob/main/.trae/skills/travel-itinerary/SKILL.md
- 本地路径：`.trae/skills/travel-itinerary/SKILL.md`

## 📁 文件结构

```
travel-itinerary/
├── README.md      # 本文件
└── SKILL.md      # Skill 核心定义
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📜 许可证

MIT License

---

*使用 SOLO + TRAE 创作于 2025-05-26*
