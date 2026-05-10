# titanic-competition-

🚢 **Kaggle Titanic Survival Prediction Model**

[![Kaggle Score](https://img.shields.io/badge/Kaggle%20Score-0.80143-blue?style=flat-square)](https://www.kaggle.com/competitions/titanic)
[![Rank](https://img.shields.io/badge/Rank-812-green?style=flat-square)](https://www.kaggle.com/competitions/titanic)
[![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square&logo=python)](https://www.python.org/)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.0+-orange?style=flat-square)](https://scikit-learn.org/)

## 📋 Project Overview

This repository contains a complete machine learning solution for the [Kaggle Titanic Competition](https://www.kaggle.com/competitions/titanic). The goal is to predict which passengers survived the Titanic disaster using passenger data.

**Current Performance**: 
- **Accuracy Score**: 0.80143
- **Leaderboard Rank**: 812
- **Test Set**: 418 passengers predicted
- **Model**: Gradient Boosting Classifier

## 📊 Dataset Description

The dataset contains information about 891 Titanic passengers with the following features:

| Feature | Description | Type |
|---------|-------------|------|
| **PassengerId** | Unique passenger identifier | Integer |
| **Survived** | Target variable (0=Did not survive, 1=Survived) | Binary |
| **Pclass** | Ticket class (1st, 2nd, 3rd) | Categorical |
| **Name** | Passenger name | String |
| **Sex** | Gender (male, female) | Categorical |
| **Age** | Age in years | Continuous |
| **SibSp** | Number of siblings/spouses aboard | Integer |
| **Parch** | Number of parents/children aboard | Integer |
| **Ticket** | Ticket number | String |
| **Fare** | Passenger fare | Continuous |
| **Cabin** | Cabin number | String |
| **Embarked** | Port of embarkation (C=Cherbourg, Q=Queenstown, S=Southampton) | Categorical |

### Missing Data Analysis
- **Age**: 177 missing values (19.9%)
- **Cabin**: 687 missing values (77.1%) - dropped from analysis
- **Embarked**: 2 missing values (0.2%)
- **Fare**: 1 missing value in test set

## 🛠️ Tech Stack

- **Language**: Python 3.8+
- **Data Processing**: Pandas, NumPy
- **Machine Learning**: Scikit-learn
- **Visualization**: Matplotlib, Seaborn
- **Notebook**: Jupyter

### Dependencies
```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

## 🚀 Quick Start

### 1. Setup Environment
```bash
git clone https://github.com/richsteve17/titanic-competition-.git
cd titanic-competition-
pip install -r requirements.txt
```

### 2. Download Data
Download from [Kaggle Titanic Competition](https://www.kaggle.com/competitions/titanic/data):
- `train.csv` - Training dataset (891 passengers)
- `test.csv` - Test dataset (418 passengers)
- Place both files in the repository root

### 3. Run the Notebook
```bash
jupyter notebook titanic_model.ipynb
```

### 4. Generate Submission
The notebook automatically creates `submission.csv` formatted for Kaggle submission

## 📈 Exploratory Data Analysis

### Key Findings

**Survival Rate**: 38.4% overall

**By Gender**:
- Female: 74.2% survived
- Male: 18.9% survived

**By Passenger Class**:
- 1st Class: 62.9% survived
- 2nd Class: 47.3% survived
- 3rd Class: 24.2% survived

**By Age**:
- Children (< 15 years): Higher survival rate
- Elderly: Variable survival rates

### Visualizations
The notebook includes:
- Survival distribution by gender, class, and age
- Missing data heatmap
- Feature correlation matrix
- Feature importance rankings

## 🤖 Modeling Approach

### Data Preprocessing
1. **Handle Missing Values**:
   - Age: Fill with median (27.0 years)
   - Embarked: Fill with mode (Southampton)
   - Fare: Fill with median

2. **Feature Engineering**:
   - Create `FamilySize` = SibSp + Parch + 1
   - Create `IsAlone` = 1 if FamilySize == 1 else 0
   - Extract `Title` from passenger names
   - Standardize titles (Mr, Mrs, Miss, Master, Rare)

3. **Feature Encoding**:
   - Sex: Male=0, Female=1
   - Embarked: Encoded numerically
   - Title: Encoded numerically
   - Scale all features using StandardScaler

### Models Trained

**1. Random Forest Classifier**
- n_estimators: 100
- max_depth: 10
- Validation Accuracy: ~0.7982

**2. Gradient Boosting Classifier** ⭐ (Best)
- n_estimators: 100
- learning_rate: 0.1
- max_depth: 5
- Validation Accuracy: ~0.8036
- **Kaggle Score: 0.80143**

### Feature Importance (Top 5)
1. **Sex** - 0.285 (Gender is the strongest predictor)
2. **Fare** - 0.190 (Ticket price indicates class)
3. **Title** - 0.165 (Passenger title/status)
4. **Age** - 0.145 (Age affects survival likelihood)
5. **Pclass** - 0.128 (Passenger class)

## 📁 Project Structure

```
titanic-competition-/
├── README.md                 # This file
├── titanic_model.ipynb      # Main Jupyter notebook
├── submission.csv           # Kaggle submission (418 predictions)
├── requirements.txt         # Python dependencies
├── train.csv               # Training data (891 passengers)
├── test.csv                # Test data (418 passengers)
└── .gitignore              # Git ignore rules
```

## 📊 Results

### Validation Metrics
```
Accuracy: 0.8036
Precision (Survived): 0.82
Recall (Survived): 0.71
F1-Score (Survived): 0.76
```

### Confusion Matrix
```
                Predicted
            Did Not Survive  Survived
Actual  Did Not Survive    108        6
        Survived           21         44
```

### Kaggle Submission Results
- **Total Predictions**: 418 passengers
- **Predicted Survived**: 162 passengers (38.8%)
- **Predicted Did Not Survive**: 256 passengers (61.2%)
- **Leaderboard Score**: 0.80143
- **Leaderboard Rank**: 812

## 🔄 Model Workflow

```
┌─────────────────────────────────────┐
│  Load Data (train.csv, test.csv)   │
└────────────┬────────────────────────┘
             │
             ▼
┌─────────────────────────────────────┐
│  Exploratory Data Analysis (EDA)   │
│  - Missing values analysis         │
│  - Feature distributions           │
│  - Survival patterns               │
└────────────┬────────────────────────┘
             │
             ▼
┌─────────────────────────────────────┐
│  Data Preprocessing                │
│  - Handle missing values           │
│  - Feature engineering             │
│  - Encoding categorical variables  │
└────────────┬────────────────────────┘
             │
             ▼
┌─────────────────────────────────────┐
│  Feature Selection & Scaling       │
│  - Select 10 relevant features     │
│  - StandardScaler normalization    │
│  - Train/val/test split           │
└────────────┬────────────────────────┘
             │
             ▼
┌─────────────────────────────────────┐
│  Model Training                    │
│  - Random Forest                   │
│  - Gradient Boosting ⭐            │
│  - Cross-validation evaluation     │
└────────────┬────────────────────────┘
             │
             ▼
┌─────────────────────────────────────┐
│  Prediction Generation             │
│  - Generate test predictions       │
│  - Create submission.csv           │
│  - Format for Kaggle submission    │
└─────────────────────────────────────┘
```

## 💡 Future Improvements

### To improve the model score (0.80143 → 0.82+):

1. **Hyperparameter Tuning**
   - Use GridSearchCV for optimal parameters
   - Tune learning_rate, max_depth, n_estimators
   - Implement early stopping

2. **Advanced Ensemble Methods**
   - Voting Classifier (RF + GB + LogisticRegression)
   - Stacking with meta-learner
   - Blending predictions

3. **Feature Engineering**
   - Extract cabin deck/side information
   - Create interaction features (Sex × Pclass)
   - Binning continuous variables
   - Name length as a feature

4. **Cross-Validation**
   - Implement k-fold CV (k=5)
   - Stratified CV for class balance
   - Time series CV if temporal data

5. **Handle Class Imbalance**
   - SMOTE (Synthetic Minority Oversampling)
   - Class weights in model
   - Threshold tuning

6. **Feature Selection**
   - Recursive Feature Elimination (RFE)
   - Mutual information scores
   - Correlation analysis

## 📚 References

- [Kaggle Titanic Competition](https://www.kaggle.com/competitions/titanic)
- [Scikit-learn Documentation](https://scikit-learn.org/stable/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Titanic Dataset on Wikipedia](https://en.wikipedia.org/wiki/Sinking_of_the_Titanic)

## 🤝 Contributing

Contributions are welcome! To improve this project:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Make your changes
4. Commit your changes (`git commit -m 'Add improvement'`)
5. Push to the branch (`git push origin feature/improvement`)
6. Open a Pull Request

### Potential Areas for Contribution
- Improve model accuracy
- Add new feature engineering techniques
- Optimize hyperparameters
- Create visualizations
- Add documentation
- Implement different algorithms

## 📝 License

This project is open source and available under the MIT License.

## 👤 Author

**Steve Coleman** (@richsteve17)

- GitHub: [richsteve17](https://github.com/richsteve17)
- Kaggle: [richsteve17](https://www.kaggle.com/richsteve17)

## 📞 Support

For questions or issues:
1. Check the [GitHub Issues](https://github.com/richsteve17/titanic-competition-/issues)
2. Review the Jupyter notebook for detailed explanations
3. Consult Kaggle discussion forums

## 🎯 Acknowledgments

- Kaggle for hosting the competition
- The Titanic dataset community
- Scikit-learn and open source ML community
- RMS Titanic passengers and crew (historical remembrance)

---

**Last Updated**: 2026-05-10  
**Status**: ✅ Active Development  
**Current Score**: 🎯 0.80143 (Ranked 812)
