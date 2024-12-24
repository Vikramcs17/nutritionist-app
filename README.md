# Indian Food Nutritionist App 🍛

A sophisticated nutrition analysis and meal recommendation system specialized for Indian cuisine. This application combines advanced data science techniques with traditional Indian food knowledge to provide personalized meal plans while considering regional preferences and nutritional requirements.

## 🎯 Key Features.

1. **Personalized Nutrition Analysis**
   - BMR (Basal Metabolic Rate) calculation using Mifflin-St Jeor Equation
   - TDEE (Total Daily Energy Expenditure) with activity level adjustments
   - Custom calorie targets based on weight goals
   - Age, gender, and body composition considerations

2. **Indian Cuisine Specialization**
   - Region-specific dish recommendations
   - State-wise cuisine analysis
   - Traditional recipe database
   - Cultural food preference integration

3. **Advanced Data Visualization**
   - Interactive Plotly charts
   - Real-time data updates
   - Comparative analysis views
   - Nutritional breakdown visualizations

4. **Machine Learning Integration**
   - RandomForest-based calorie prediction
   - Feature importance analysis
   - Cross-validated model performance
   - Adaptive recommendation system

## 🚀 Detailed Installation Guide

### System Requirements
- Python 3.7+ (3.8 recommended)
- 4GB RAM minimum (8GB recommended)
- 500MB free disk space
- Windows/Linux/MacOS compatible

### Step-by-Step Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/yourusername/nutritionist-app.git
   cd nutritionist-app
   ```

2. **Create Virtual Environment**
   ```bash
   python -m venv venv
   ```

3. **Activate Virtual Environment**
   - Windows:
     ```bash
     venv\Scripts\activate
     ```
   - Unix/MacOS:
     ```bash
     source venv/bin/activate
     ```

4. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```
   
   Key dependencies include:
   - streamlit==1.24.0
   - pandas==1.5.3
   - numpy==1.24.3
   - scikit-learn==1.2.2
   - plotly==5.15.0

5. **Verify Installation**
   ```bash
   python -c "import streamlit; import pandas; import sklearn; print('Installation successful!')"
   ```

6. **Run Application**
   ```bash
   streamlit run indian_food_app.py
   ```

## 📊 Technical Architecture

### 1. Data Layer
#### Dataset Structure
- **indian_food.csv**
  ```
  Columns:
  - Food Name (string)
  - State (string)
  - Total Calories (float)
  - Total Carbs (float)
  - Total Fats (float)
  - Total Protein (float)
  - Total Sugar (float)
  - Total Sodium (float)
  - Allergic Ingredients (string)
  - Vitamins (string)
  ```

#### Data Preprocessing Pipeline
```python
def preprocess_data(df):
    # Numeric conversion
    numeric_columns = ['Total Calories', 'Total Carbs', 'Total Fats', 
                      'Total Protein', 'Total Sugar', 'Total Sodium']
    df[numeric_columns] = df[numeric_columns].apply(pd.to_numeric, errors='coerce')
    
    # Missing value handling
    df = df.dropna(subset=numeric_columns)
    
    # Feature scaling
    scaler = StandardScaler()
    df[numeric_columns] = scaler.fit_transform(df[numeric_columns])
    
    return df, scaler
```

### 2. Machine Learning Component
#### Model Architecture
```python
def train_model(X, y):
    # Model configuration
    model = RandomForestRegressor(
        n_estimators=100,
        max_depth=None,
        min_samples_split=2,
        min_samples_leaf=1,
        random_state=42
    )
    
    # Training
    model.fit(X, y)
    
    return model
```

#### Feature Engineering
- Nutrient ratio calculations
- Categorical encoding for states
- Feature scaling and normalization
- Cross-feature generation

### 3. Nutrition Calculator
#### BMR Calculation
```python
def calculate_bmr(weight, height, age, gender):
    """
    Mifflin-St Jeor Equation:
    Men: BMR = 10W + 6.25H - 5A + 5
    Women: BMR = 10W + 6.25H - 5A - 161
    """
    if gender == 'Male':
        return 88.362 + (13.397 * weight) + (4.799 * height) - (5.677 * age)
    return 447.593 + (9.247 * weight) + (3.098 * height) - (4.330 * age)
```

#### TDEE Calculation
```python
def calculate_tdee(bmr, activity_level):
    multipliers = {
        'Sedentary': 1.2,          # Little/no exercise
        'Lightly active': 1.375,    # Light exercise 1-3 days/week
        'Moderately active': 1.55,  # Moderate exercise 3-5 days/week
        'Very active': 1.725,       # Heavy exercise 6-7 days/week
        'Super active': 1.9         # Very heavy exercise/physical job
    }
    return bmr * multipliers[activity_level]
```

### 4. Meal Recommendation Engine
#### Algorithm Overview
1. **Initial Filtering**
   - State preference filtering
   - Calorie range calculation (±50% of target)
   - Allergen exclusion

2. **Scoring System**
   - Calorie match score (40%)
   - Nutrient balance score (30%)
   - Regional preference score (20%)
   - Variety score (10%)

3. **Selection Process**
   ```python
   def get_meal_recommendations(df, target_calories, state=None):
       # Calculate meal-wise targets
       meal_targets = {
           'Breakfast': target_calories * 0.3,
           'Lunch': target_calories * 0.4,
           'Dinner': target_calories * 0.3
       }
       
       recommendations = {}
       for meal, target in meal_targets.items():
           filtered_df = filter_by_constraints(df, target, state)
           scored_df = calculate_meal_scores(filtered_df, target)
           recommendations[meal] = select_best_matches(scored_df)
       
       return recommendations
   ```

## 📈 Visualization Components

### 1. Distribution Charts
- Food type distribution using Plotly bar charts
- State-wise calorie distribution
- Nutrient composition pie charts
- Protein vs. Calories scatter plots

### 2. Interactive Elements
- Dynamic filters for state selection
- Real-time calculation updates
- Responsive chart resizing
- Tooltip information display

## 🔍 Usage Scenarios

### 1. Weight Loss Plan
```python
# Example inputs
profile = {
    'weight': 75,
    'height': 170,
    'age': 30,
    'gender': 'Male',
    'activity_level': 'Moderately active',
    'goal': 'Lose weight'
}

# Calculation flow
bmr = calculate_bmr(profile['weight'], profile['height'], 
                   profile['age'], profile['gender'])
tdee = calculate_tdee(bmr, profile['activity_level'])
target_calories = tdee - 500  # Caloric deficit
```

### 2. Maintenance Plan
- Balanced calorie distribution
- Nutrient-focused recommendations
- Regional cuisine integration

### 3. Weight Gain Plan
- Increased calorie targets
- Protein-rich recommendations
- Balanced nutrient distribution

## 🛠️ Advanced Features

### 1. Nutrient Tracking
- Macro and micronutrient monitoring
- Vitamin and mineral tracking
- Allergen identification

### 2. Regional Customization
- State-specific dish recommendations
- Cultural preference consideration
- Traditional recipe alternatives

### 3. Performance Optimization
- Data caching strategies
- Efficient filtering algorithms
- Response time optimization

## 📝 Development Guidelines

### Code Style
- PEP 8 compliance
- Type hints usage
- Docstring documentation
- Clean code principles

### Testing
```python
# Example test case
def test_bmr_calculation():
    assert abs(calculate_bmr(70, 170, 30, 'Male') - 1686.2) < 0.1
    assert abs(calculate_bmr(60, 160, 25, 'Female') - 1357.5) < 0.1
```

### Error Handling
```python
def safe_calculation(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        try:
            return func(*args, **kwargs)
        except ValueError as e:
            st.error(f"Calculation error: {str(e)}")
        except Exception as e:
            st.error(f"Unexpected error: {str(e)}")
    return wrapper
```

## 🔄 Update and Maintenance

### Version Control
- Git-based version control
- Feature branch workflow
- Semantic versioning

### Data Updates
- Regular dataset updates
- Validation procedures
- Backup strategies

## 🤝 Contributing Guidelines

### Submission Process
1. Fork repository
2. Create feature branch
3. Implement changes
4. Submit pull request

### Code Review Criteria
- Functionality testing
- Code style compliance
- Documentation completeness
- Performance impact

## 📄 License and Credits

### MIT License
Copyright (c) 2023 [Your Name]

### Acknowledgments
- Indian cuisine database contributors
- Streamlit community
- Open-source contributors

## 📚 Additional Resources

### Documentation
- [Streamlit Documentation](https://docs.streamlit.io/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Scikit-learn Documentation](https://scikit-learn.org/stable/documentation.html)

### Tutorials
1. Basic Usage Guide
2. Advanced Features Tutorial
3. Customization Guide

### Support
- GitHub Issues
- Email Support
- Community Forum
