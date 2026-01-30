# Linear Regression Architecture Workshop

A comprehensive implementation of linear regression using Object-Oriented Programming principles, featuring data collection from multiple sources, from-scratch gradient descent implementation, and extensive exploratory data analysis.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Setup Instructions](#setup-instructions)
- [Usage Guide](#usage-guide)
- [Implementation Details](#implementation-details)
- [Results](#results)
- [Requirements](#requirements)
- [Next Steps](#next-steps)

## 🎯 Overview

This project demonstrates a complete machine learning pipeline for housing price prediction, covering:

1. **Data Collection**: Multi-source data collection system using OOP
2. **Exploratory Data Analysis**: Comprehensive statistical analysis and visualization
3. **Linear Regression**: Both from-scratch and scikit-learn implementations
4. **Model Evaluation**: RMSE, MAE, R² metrics with visualizations

## ✨ Features

### 1. Multi-Source Data Collection System

**Notebook**: `notebooks/fetch_dataset.ipynb`

An OOP-based data collection framework supporting three data source types:

#### **A. CSV Data Source**
- Fetches California Housing dataset from scikit-learn
- Automatic CSV export for persistence
- Location: `data/raw/california_housing.csv`
- **20,640 samples** with 9 features

#### **B. API Data Source**
- Integrates with Toronto Open Data Portal
- Fetches Ontario housing data via REST API
- Fallback to synthetic data generation
- Location: `data/raw/ontario_housing_api.csv`
- Demonstrates real-world web service integration

#### **C. Database Data Source**
- SQLite database implementation (portable)
- Custom SQL query support
- CRUD operations
- Database: `data/raw/housing.db`
- Easily extensible to PostgreSQL/MySQL

#### **Architecture**

```
DataSource (Abstract Base Class)
├── CSVDataSource
├── APIDataSource
└── DatabaseDataSource

HousingDataCollector (Orchestrator)
└── Manages multiple data sources

EDAAnalyzer
└── Performs exploratory data analysis
```

**Key Features**:
- ✅ Abstract base class design pattern
- ✅ Data validation for each source
- ✅ Automatic column standardization
- ✅ Comprehensive EDA capabilities
- ✅ Summary statistics
- ✅ Distribution plots
- ✅ Correlation heatmaps
- ✅ Cross-dataset comparisons

### 2. Univariate Linear Regression

**Notebook**: `notebooks/univariate_linear_regression.ipynb`

Complete implementation of linear regression from mathematical foundations to production-ready code.

#### **Problem Statement**
Predict **median house value** using **median income** as the single predictor.

#### **Mathematical Foundation**

**Hypothesis Function**:
```
h_θ(x) = θ₀ + θ₁x
```

**Cost Function (MSE)**:
```
J(θ₀, θ₁) = (1/2m) Σ(h_θ(x⁽ⁱ⁾) - y⁽ⁱ⁾)²
```

**Gradient Descent Updates**:
```
θ₀ := θ₀ - α(1/m)Σ(h_θ(x⁽ⁱ⁾) - y⁽ⁱ⁾)
θ₁ := θ₁ - α(1/m)Σ(h_θ(x⁽ⁱ⁾) - y⁽ⁱ⁾)·x⁽ⁱ⁾
```

#### **Implementation Highlights**

**From-Scratch Implementation**:
- Complete `LinearRegressionScratch` class
- Gradient descent optimization
- Cost history tracking
- Configurable learning rate and iterations
- Mathematical validation

**Scikit-learn Implementation**:
- Standard library comparison
- Validates from-scratch implementation
- Performance benchmarking

#### **Preprocessing Pipeline**
1. ✅ Missing value detection
2. ✅ Train/test split (80/20)
3. ✅ Feature standardization (StandardScaler)
4. ✅ Data validation

#### **Evaluation Metrics**
- **RMSE** (Root Mean Squared Error): ~0.73
- **MAE** (Mean Absolute Error): ~0.53
- **R²** (Coefficient of Determination): ~0.47

#### **Visualizations**
1. **Cost Convergence**: Gradient descent optimization path
2. **Regression Line**: Model fit vs actual data
3. **Residual Analysis**: Error distribution and patterns
4. **Predicted vs Actual**: Model accuracy visualization
5. **Performance Comparison**: From-scratch vs scikit-learn

## 📁 Project Structure

```
LinearRegressionArchitecture_Workshop/
│
├── README.md                          # This file
├── requirements.txt                   # Python dependencies
├── .gitignore                         # Git ignore rules
│
├── configs/
│   └── experiment_config.yaml         # Configuration file
│
├── data/
│   ├── raw/                           # Raw data files
│   │   ├── california_housing.csv     # California Housing dataset
│   │   ├── ontario_housing_api.csv    # Ontario housing data (API)
│   │   └── housing.db                 # SQLite database
│   │
│   └── processed/                     # Processed data
│       ├── csv_file_california_processed.csv
│       ├── web_api_ontario_processed.csv
│       ├── sqlite_database_combined_processed.csv
│       └── univariate_regression_results.csv
│
├── notebooks/
│   ├── fetch_dataset.ipynb            # Multi-source data collection
│   ├── univariate_linear_regression.ipynb  # Univariate LR implementation
│   ├── EDA.ipynb                      # Exploratory Data Analysis
│   └── linear_regression.ipynb        # Additional experiments
│
├── src/
│   ├── data_loader.py                 # Data loading utilities
│   ├── preprocessing.py               # Preprocessing functions
│   ├── model.py                       # Model implementations
│   └── evaluation.py                  # Evaluation metrics
│
└── experiments/
    └── results.csv                    # Experiment results
```

## 🚀 Setup Instructions

### Prerequisites

- Python 3.8 or higher
- pip package manager
- Jupyter Notebook or JupyterLab

### Installation

1. **Clone the repository**:
   ```bash
   cd LinearRegressionArchitecture_Workshop
   ```

2. **Create a virtual environment** (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Verify installation**:
   ```bash
   python -c "import pandas, numpy, sklearn, matplotlib, seaborn; print('✓ All packages installed')"
   ```

## 📖 Usage Guide

### 1. Data Collection

**Run the data collection notebook**:
```bash
jupyter notebook notebooks/fetch_dataset.ipynb
```

**What it does**:
- Fetches California Housing data from scikit-learn
- Attempts to fetch Ontario housing data from Toronto Open Data API
- Creates SQLite database with housing data
- Performs comprehensive EDA on all datasets
- Exports processed data to `data/processed/`

**Expected Output**:
- 3 datasets loaded successfully
- Summary statistics for each dataset
- Distribution plots
- Correlation heatmaps
- Dataset comparison visualizations

### 2. Univariate Linear Regression

**Run the regression notebook**:
```bash
jupyter notebook notebooks/univariate_linear_regression.ipynb
```

**What it does**:
- Loads California Housing data
- Preprocesses features (standardization, train/test split)
- Trains from-scratch linear regression using gradient descent
- Trains scikit-learn linear regression for comparison
- Evaluates both models (RMSE, MAE, R²)
- Generates comprehensive visualizations
- Saves predictions to `data/processed/univariate_regression_results.csv`

**Expected Output**:
- Training complete with learned parameters
- Cost convergence visualization
- Model comparison metrics
- Regression line plots
- Residual analysis
- Performance summary

### 3. Quick Start (All-in-One)

```bash
# Start Jupyter
jupyter notebook

# Navigate to notebooks/ and run in order:
# 1. fetch_dataset.ipynb
# 2. univariate_linear_regression.ipynb
```

## 🔬 Implementation Details

### Data Collection System

**Class Hierarchy**:

```python
class DataSource(ABC):
    """Abstract base class for all data sources"""
    - fetch_data() -> pd.DataFrame
    - validate_data() -> bool
    - get_info() -> Dict
    - standardize_columns() -> pd.DataFrame

class CSVDataSource(DataSource):
    """CSV file data source"""
    - Loads from sklearn or CSV file
    - Automatic persistence

class APIDataSource(DataSource):
    """Web API data source"""
    - REST API integration
    - Fallback data generation
    - JSON to DataFrame conversion

class DatabaseDataSource(DataSource):
    """Database data source"""
    - SQLite/PostgreSQL/MySQL support
    - Custom SQL queries
    - Transaction management

class HousingDataCollector:
    """Orchestrates multiple data sources"""
    - add_source()
    - collect_all()
    - get_summary()

class EDAAnalyzer:
    """Exploratory data analysis"""
    - summary_statistics()
    - plot_distributions()
    - plot_correlations()
    - compare_datasets()
```

### Linear Regression Implementation

**From-Scratch Class**:

```python
class LinearRegressionScratch:
    """Linear regression with gradient descent"""
    
    def __init__(self, learning_rate=0.01, n_iterations=1000):
        self.learning_rate = learning_rate
        self.n_iterations = n_iterations
        self.theta0 = 0  # Intercept
        self.theta1 = 0  # Slope
        self.cost_history = []
    
    def fit(self, X, y):
        """Train using gradient descent"""
        # Gradient descent optimization
        for i in range(self.n_iterations):
            predictions = self.theta0 + self.theta1 * X
            errors = predictions - y
            
            # Update parameters
            self.theta0 -= self.learning_rate * (1/m) * sum(errors)
            self.theta1 -= self.learning_rate * (1/m) * sum(errors * X)
    
    def predict(self, X):
        """Make predictions"""
        return self.theta0 + self.theta1 * X
```

**Key Algorithms**:
- **Gradient Descent**: Iterative optimization
- **StandardScaler**: Feature normalization
- **Train/Test Split**: 80/20 ratio
- **Cross-validation**: Ready for implementation

## 📊 Results

### Dataset Statistics

| Dataset | Rows | Columns | Source Type |
|---------|------|---------|-------------|
| California Housing | 20,640 | 9 | CSV (scikit-learn) |
| Ontario Housing | 1,000 | 8 | API (Toronto Open Data) |
| Combined Housing | 500 | 6 | SQLite Database |

### Model Performance

| Metric | From-Scratch | Scikit-learn | Difference |
|--------|--------------|--------------|------------|
| **RMSE** | 0.7338 | 0.7338 | ~0.0000 |
| **MAE** | 0.5329 | 0.5329 | ~0.0000 |
| **R²** | 0.4734 | 0.4734 | ~0.0000 |

**Key Findings**:
- ✅ From-scratch implementation matches scikit-learn exactly
- ✅ Gradient descent converges successfully
- ✅ Median income explains ~47% of house value variance
- ✅ Strong positive correlation (r = 0.69) between income and house value

### Visualizations Generated

1. **Data Collection Notebook**:
   - Distribution plots for all features
   - Correlation heatmaps
   - Cross-dataset comparisons
   - Summary statistics tables

2. **Regression Notebook**:
   - Cost function convergence (gradient descent)
   - Regression line vs actual data
   - Residual plots (scatter + histogram)
   - Predicted vs actual scatter plots
   - Performance comparison bar charts

## 📦 Requirements

### Core Dependencies

```
pandas>=1.5.0          # Data manipulation
numpy>=1.23.0          # Numerical computing
scikit-learn>=1.2.0    # Machine learning
matplotlib>=3.6.0      # Plotting
seaborn>=0.12.0        # Statistical visualization
```

### Additional Dependencies

```
plotly>=5.0.0          # Interactive plots
requests>=2.28.0       # HTTP requests
httpx>=0.23.0          # Async HTTP
SQLAlchemy>=2.0.0      # Database ORM
psycopg2-binary>=2.9.0 # PostgreSQL adapter
pyyaml>=6.0            # YAML parsing
jupyter>=1.0.0         # Jupyter notebooks
ipykernel>=6.0.0       # Jupyter kernel
```

**Install all dependencies**:
```bash
pip install -r requirements.txt
```

## 🎓 Learning Outcomes

This project demonstrates:

1. **OOP Design Patterns**:
   - Abstract base classes
   - Inheritance and polymorphism
   - Encapsulation
   - Single Responsibility Principle

2. **Machine Learning Fundamentals**:
   - Gradient descent optimization
   - Cost function minimization
   - Feature scaling
   - Model evaluation metrics

3. **Data Engineering**:
   - Multi-source data collection
   - ETL pipeline design
   - Database integration
   - API consumption

4. **Software Engineering Best Practices**:
   - Clean code organization
   - Comprehensive documentation
   - Version control
   - Reproducibility

## 🔮 Next Steps

### Planned Features

1. **Multivariate Linear Regression**:
   - Multiple feature selection
   - Feature engineering
   - Regularization (Ridge, Lasso, ElasticNet)

2. **Advanced Models**:
   - Polynomial regression
   - Feature interactions
   - Non-linear transformations

3. **Model Optimization**:
   - Hyperparameter tuning
   - Cross-validation
   - Grid search / Random search

4. **Production Readiness**:
   - Model serialization (pickle/joblib)
   - REST API endpoint
   - Docker containerization
   - CI/CD pipeline

5. **Advanced Visualizations**:
   - Interactive Plotly dashboards
   - 3D surface plots
   - Feature importance analysis

6. **Database Enhancements**:
   - PostgreSQL integration
   - Connection pooling
   - Query optimization

## 📝 Notes

### Data Sources

- **California Housing**: Built-in scikit-learn dataset (real data from 1990 census)
- **Ontario Housing**: Toronto Open Data Portal (may use synthetic data as fallback)
- **Database**: SQLite for portability (production should use PostgreSQL)

### Model Assumptions

Linear regression assumes:
1. Linear relationship between features and target
2. Independence of observations
3. Homoscedasticity (constant variance)
4. Normal distribution of residuals

**Validation**:
- ✅ Linear relationship confirmed (scatter plots)
- ✅ Independence assumed (cross-sectional data)
- ⚠️ Heteroscedasticity detected (residual analysis)
- ✅ Residuals approximately normal

## 🤝 Contributing

This is an educational project for CSCN8010. For questions or suggestions:

1. Review existing notebooks
2. Check documentation
3. Run example notebooks
4. Experiment with parameters

## 📄 License

This project is for educational purposes as part of CSCN8010 coursework.

## 🙏 Acknowledgments

- **Dataset**: California Housing dataset from scikit-learn
- **API**: Toronto Open Data Portal
- **Libraries**: scikit-learn, pandas, numpy, matplotlib, seaborn

---

**Course**: CSCN8010 - Machine Learning  
**Institution**: Conestoga College  
**Workshop**: Linear Regression Architecture  
**Date**: January 2026

---

## 📞 Contact

For questions about this implementation, please refer to the course materials or consult with the instructor.

---

**Last Updated**: January 30, 2026  
**Version**: 1.0.0  
**Status**: ✅ Session 1 Deliverables Complete
