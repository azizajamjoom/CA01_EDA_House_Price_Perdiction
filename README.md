# CA01 – House Price EDA & Preprocessing

This repository contains an exploratory data analysis (EDA) and preprocessing workflow for the Ames Housing dataset, with **SalePrice** as the target variable. The goal of this project is to understand data distributions, relationships between key features and house prices, handle missing values, and identify potential collinearity issues before building predictive models.

---

## Dataset

The Ames Housing training dataset is loaded directly from GitHub and includes housing characteristics such as:

- Living area square footage  
- Overall house quality  
- Basement size  
- Garage capacity and area  
- Year built and remodeled  
- Various structural and neighborhood features  

Target variable:
- **SalePrice** – final sale price of each house

---

## Project Workflow

### 1. Exploratory Data Analysis (EDA)

The notebook explores:

- Basic dataset structure and summary statistics  
- Missing value patterns across features  
- Distribution of house prices  
- Key visual relationships, including:
  - SalePrice distribution (histogram)  
  - Living area vs SalePrice (scatter plot)  
  - Overall quality vs SalePrice (boxplot)  
  - Living area distribution  

These visualizations help identify skewness, outliers, and strong predictors of housing prices.

---

### 2. Data Preprocessing

Missing values are handled using domain-informed strategies:

#### Categorical features:
Missing values are filled with `"None"` for variables where missing indicates the absence of a feature (e.g., no garage, no basement, no pool).

#### Numerical features:
- `LotFrontage` filled using median values  
- `MasVnrArea` filled with 0 where missing  

This ensures the dataset is clean and ready for modeling.

---

### 3. Post-Processing: Correlation & Collinearity Analysis

- A correlation matrix is computed for numerical features  
- A small table highlights features strongly correlated with `SalePrice` (|correlation| > 0.5)  
- This step helps:
  - Identify top predictors  
  - Flag highly related features that may introduce collinearity in models  

---

## YData Profiling Report (Important Note)

The project uses **ydata-profiling** to generate an automated exploratory report.  

However, interactive widget metadata created by this library can cause GitHub to display an **“Invalid Notebook”** error when rendering the `.ipynb` file.

### Solution used in this repository:

- The YData profiling code is commented out in the notebook for GitHub compatibility  
- The report can be generated locally and exported as an HTML file using:

```python
from ydata_profiling import ProfileReport

profile = ProfileReport(df, title="Housing Data Report", explorative=True)
profile.to_file("report.html")
