---
name: "recipe-nutritionist"
description: "Analyzes recipe ingredients and generates nutrition facts, calorie calculations, and health recommendations. Invoke when user wants to know nutrition info, calculate calories, or get healthy eating advice."
---

# 🍳 Recipe Nutritionist

## 🎯 Overview
A specialized skill for analyzing recipe ingredients and generating comprehensive nutrition facts. Calculate calories, macronutrients, vitamins, and get personalized health recommendations based on dietary goals.

## 💡 When to Use
- Calculate calories and nutrition for any recipe
- Get healthy eating recommendations
- Track daily nutrition intake
- Plan meals for specific diets (weight loss, muscle gain, diabetes)

## ⚔️ Execution Rules
1. **Ingredient Parsing**: Extract individual ingredients and quantities from recipe
2. **Nutrition Lookup**: Match ingredients to nutrition database
3. **Health Analysis**: Evaluate against dietary guidelines
4. **Recommendation Engine**: Generate personalized suggestions

## 🛠️ Usage

### Step 1: Provide Recipe or Ingredients
User provides a recipe or list of ingredients

### Step 2: Run the Analyzer
```python
# Basic nutrition analysis
def analyze_nutrition(ingredients):
    """
    Analyze nutrition facts for given ingredients
    
    Args:
        ingredients: list of {"name": str, "amount": float, "unit": str}
    
    Returns:
        dict with nutrition breakdown
    """
    nutrition_data = {
        "total_calories": 0,
        "macros": {"protein": 0, "carbs": 0, "fat": 0},
        "fiber": 0,
        "sodium": 0
    }
    
    for item in ingredients:
        # Lookup nutrition per 100g
        nutrition_per_100g = get_nutrition_data(item["name"])
        
        # Calculate based on amount
        amount_grams = convert_to_grams(item["amount"], item["unit"])
        multiplier = amount_grams / 100
        
        nutrition_data["total_calories"] += nutrition_per_100g["calories"] * multiplier
        nutrition_data["macros"]["protein"] += nutrition_per_100g["protein"] * multiplier
        nutrition_data["macros"]["carbs"] += nutrition_per_100g["carbs"] * multiplier
        nutrition_data["macros"]["fat"] += nutrition_per_100g["fat"] * multiplier
    
    return nutrition_data

# Example usage
ingredients = [
    {"name": "鸡胸肉", "amount": 200, "unit": "g"},
    {"name": "西兰花", "amount": 100, "unit": "g"},
    {"name": "糙米", "amount": 150, "unit": "g"}
]

result = analyze_nutrition(ingredients)
print(f"Total Calories: {result['total_calories']} kcal")
print(f"Protein: {result['macros']['protein']}g")
```

### Step 3: Get Health Report
```markdown
# 🍽️ Nutrition Report

## 📊 Nutrition Facts (per serving)
| Nutrient | Amount | % Daily Value |
|----------|--------|---------------|
| Calories | 450 kcal | 22% |
| Protein | 35g | 70% |
| Carbs | 45g | 15% |
| Fat | 12g | 15% |
| Fiber | 6g | 24% |

## ⚠️ Health Analysis
- ✅ High protein - Good for muscle building
- ✅ Low sodium - Heart healthy
- ⚡ Moderate carbs - Suitable for active lifestyle

## 💡 Recommendations
- Add some healthy fats (avocado, olive oil) for better absorption
- Consider adding leafy greens for more vitamins
```

## 🎯 Supported Features
- ✅ Ingredient parsing and quantity conversion
- ✅ Calorie and macronutrient calculation
- ✅ Daily value percentage calculation
- ✅ Health analysis and warnings
- ✅ Personalized recommendations
- ✅ Dietary goal tracking

## ⚠️ Limitations
- Nutrition data is approximate
- Some obscure ingredients may not be in database
- Individual allergies not automatically detected

## 🚀 Trigger Keywords
- "营养分析"
- "计算热量"
- "这个菜多少卡路里"
- "nutrition analyzer"
- "calorie counter"
