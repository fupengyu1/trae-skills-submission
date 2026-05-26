---
name: "travel-itinerary"
description: "Generates comprehensive travel itineraries with day-by-day plans, hotel recommendations, and transportation options. Invoke when user wants to plan a trip, organize travel schedule, or get destination suggestions."
---

# ✈️ Travel Itinerary Planner

## 🎯 Overview
An intelligent travel planning assistant that generates comprehensive trip itineraries. Input your destination, dates, and preferences to get personalized day-by-day plans, hotel recommendations, dining suggestions, and transportation options.

## 💡 When to Use
- Plan a new trip or vacation
- Organize travel schedule
- Get destination recommendations
- Find best routes and transportation
- Create packing checklists

## ⚔️ Execution Rules
1. **Destination Research**: Gather information about location
2. **Preference Analysis**: Understand travel style and interests
3. **Route Optimization**: Plan efficient daily schedules
4. **Budget Planning**: Estimate costs and suggest options
5. **Checklist Generation**: Create packing and preparation lists

## 🛠️ Usage

### Step 1: Provide Trip Details
User specifies destination, dates, budget, and preferences

### Step 2: Generate Itinerary
```python
def generate_itinerary(destination, days, budget="medium", style="balanced"):
    """
    Generate a comprehensive travel itinerary
    
    Args:
        destination: str (city or region name)
        days: int (number of days)
        budget: str (low/medium/high)
        style: str (relaxed/balanced/active)
    
    Returns:
        dict with daily plans and recommendations
    """
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
    
    # Research destination
    info = get_destination_info(destination)
    
    # Generate daily plans based on style
    for day in range(1, days + 1):
        daily_plan = create_daily_plan(
            destination=destination,
            day=day,
            style=style,
            weather=get_weather_forecast(destination, day)
        )
        itinerary["daily_plans"].append(daily_plan)
    
    # Add hotel recommendations
    itinerary["hotels"] = get_hotel_recommendations(
        destination, budget, days
    )
    
    # Add dining suggestions
    itinerary["restaurants"] = get_restaurant_recommendations(
        destination, style
    )
    
    # Generate tips
    itinerary["tips"] = get_local_tips(destination)
    
    return itinerary

# Example
result = generate_itinerary(
    destination="杭州",
    days=3,
    budget="medium",
    style="balanced"
)
```

### Step 3: Get Detailed Plan
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

## 🎯 Supported Features
- ✅ Day-by-day itinerary generation
- ✅ Theme-based trip planning
- ✅ Hotel and restaurant recommendations
- ✅ Transportation suggestions
- ✅ Budget estimation
- ✅ Packing checklist generation
- ✅ Weather-aware planning

## ⚠️ Limitations
- Real-time pricing not available
- Booking functionality not included
- Weather forecasts are approximate

## 🚀 Trigger Keywords
- "旅行规划"
- "制定行程"
- "旅游攻略"
- "travel planner"
- "trip itinerary"
- "去XX玩几天"
