# Indian Food Nutritionist App 🍛

A comprehensive nutrition analysis and meal recommendation system specialized for Indian cuisine, combining data science with traditional Indian food knowledge.

## 🚀 Getting Started

### Prerequisites
- Python 3.7 or higher
- pip package manager

### Installation
1. Create a virtual environment:
   ```bash
   python -m venv venv
   ```

2. Activate the virtual environment:
   - Windows:
     ```bash
     venv\Scripts\activate
     ```
   - Unix/MacOS:
     ```bash
     source venv/bin/activate
     ```

3. Install required packages:
   ```bash
   pip install -r requirements.txt
   ```

4. Run the application:
   ```bash
   streamlit run app.py             # For general nutrition app
   # or
   streamlit run indian_food_app.py # For Indian cuisine specific app
   ```

## 📊 Project Components

### 1. Data Management
- **Datasets**:
  - `nutrients_csvfile.csv`: General nutrition database
  - `indian_food.csv`: Specialized Indian cuisine database with regional information

- **Preprocessing**:
  - Numeric data conversion
  - Missing value handling
  - Data validation

### 2. Machine Learning Components
- **Model**: RandomForest Regressor
- **Features**: 
  - Total Carbohydrates
  - Total Fats
  - Total Protein
  - Total Sugar
  - Total Sodium
- **Target**: Calorie prediction
- **Evaluation Metrics**: MSE, R² Score

### 3. Nutrition Calculation System
- **BMR (Basal Metabolic Rate)**:
  - Gender-specific calculations
  - Accounts for weight, height, and age
  
- **TDEE (Total Daily Energy Expenditure)**:
  - Activity level adjustments
  - Customized multipliers for different lifestyle types

- **Goal-Based Calculations**:
  - Weight loss (-500 calories)
  - Weight maintenance
  - Weight gain (+500 calories)

### 4. Meal Recommendation System
- **Personalization Factors**:
  - Daily calorie targets
  - State-specific cuisine preferences
  - Meal-time distribution (30-40-30 split)

- **Selection Criteria**:
  - Calorie matching within ±50% range
  - Nutritional balance
  - Regional cuisine preferences

### 5. Visualization Dashboard
- **Interactive Charts**:
  - Food type distribution
  - State-wise calorie analysis
  - Nutrient composition breakdown
  - Protein vs. Calories correlation

- **User Interface**:
  - Personal profile inputs
  - Dietary preference selection
  - Real-time calculation updates
  - Comprehensive meal planning display

## 🎯 Features

1. **Personalized Meal Planning**
   - Custom calorie calculations
   - Activity level adjustments
   - Goal-based recommendations

2. **Regional Cuisine Focus**
   - State-specific dish recommendations
   - Cultural food preferences
   - Traditional recipe analysis

3. **Nutritional Analysis**
   - Detailed macro breakdown
   - Vitamin content information
   - Allergen warnings

4. **Interactive Experience**
   - Real-time calculations
   - Dynamic visualizations
   - Immediate feedback system

## 💻 Technical Implementation

### Core Functions:
```python
# Calorie Calculations
calculate_bmr(weight, height, age, gender)
calculate_tdee(bmr, activity_level)
calculate_target_calories(tdee, goal)

# Meal Planning
get_meal_recommendations(df, target_calories, state)
display_meals(meals, meal_type, target_calories)

# Data Processing
load_and_preprocess_data()
train_model(df)
```

## 🔍 Usage Example

1. Enter personal details:
   - Weight, height, age
   - Gender and activity level
   - Weight management goals

2. Select preferences:
   - Preferred state cuisine
   - Dietary restrictions

3. Receive recommendations:
   - Personalized meal plans
   - Nutritional breakdown
   - Alternative options

## 🛠️ Future Enhancements

1. **Extended Features**
   - User profile saving
   - More regional cuisines
   - Recipe modifications

2. **Technical Improvements**
   - Advanced ML models
   - More sophisticated recommendations
   - Enhanced visualization options

## 📝 Notes

- Calorie calculations use standard formulas
- Recommendations consider both nutrition and regional preferences
- System provides alternatives when exact matches aren't found

## 🤝 Contributing

Feel free to:
- Report bugs
- Suggest enhancements
- Submit pull requests

## 📄 License

This project is open source and available under the MIT License.
