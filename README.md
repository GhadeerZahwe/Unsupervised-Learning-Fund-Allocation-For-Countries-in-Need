# Unsupervised Learning for Fund Allocation for Countries in Need

## Description
This project implements an **Unsupervised Machine Learning pipeline** to categorize countries based on socio-economic and health indicators to help allocate humanitarian aid efficiently. 

We use **clustering algorithms** to group countries into clusters depending on their conditions, which allows **HELP International** to make data-driven decisions for fund allocation.

The pipeline includes:  
- **Exploratory Data Analysis (EDA)**  
- **Feature Engineering & Scaling**  
- **Principal Component Analysis (PCA)** for dimensionality reduction  
- **Clustering Algorithms:**  
  - K-Means  
  - DBSCAN  
  - Agglomerative Hierarchical Clustering  

---

## Dataset
The dataset (`country_data.csv`) is sourced from Kaggle: [Resource Link](https://www.kaggle.com/datasets/rohan0301/unsupervised-learning-on-country-data?resource=download)  

### Attributes:
- **country** : Name of the country  
- **child_mort** : Deaths of children under 5 years of age per 1000 live births  
- **exports** : Exports of goods and services per capita (% of GDP per capita)  
- **health** : Total health spending per capita (% of GDP per capita)  
- **imports** : Imports of goods and services per capita (% of GDP per capita)  
- **Income** : Net income per person  
- **Inflation** : Annual GDP growth rate  
- **life_expec** : Average life expectancy of a newborn child  
- **total_fer** : Number of children per woman  
- **gdpp** : GDP per capita  

---

## Problem Statement
HELP International has raised $10 million and wants to **strategically allocate funds** to countries in most need. Using socio-economic and health indicators, we cluster countries to identify **economically backward nations** that should receive assistance during disasters or crises.

**Aim:**  
- Cluster countries based on numerical features.  
- Provide insights for fund allocation using unsupervised learning.  

---

## Exploratory Data Analysis (EDA)

### Feature Distributions
- **life_expec**: Negatively skewed  
- **health**: Normally distributed  
- Other features: Positively skewed  

### Key Insights on Economically Backward Countries:
- Low income per capita  
- High population leading to resource scarcity  
- Poor health and educational infrastructure  
- High child mortality and fertility rates  

### Examples from Data
- **Haiti**: Highest child mortality  
- **Singapore, Luxembourg**: Highest exports and imports  
- **Qatar**: Highest per capita income  
- **African countries**: Generally lower income, life expectancy, and health spending  

### Correlations
- **child_mort** increases when **income, gdpp, exports** decrease  
- **income** and **gdpp** highly correlated (0.9)  
- **Exports** positively impact **gdpp, income, imports**  
- Features categorized into three groups:  
  1. **Health:** `child_mort`, `health`, `life_expec`, `total_fer`  
  2. **Trade:** `imports`, `exports`  
  3. **Finance:** `income`, `inflation`, `gdpp`  

---

## Feature Engineering & Data Scaling
- **Normalization:** Applied to Health, Trade, and Finance features due to non-normal distribution  
- **Standardization:** Not applied since most features were non-normally distributed  

---

## Dimensionality Reduction (PCA)
- PCA applied to reduce feature dimensions while retaining **95% variance**  
- **Selected 2 principal components** for modeling  

---

## Modeling

### K-Means Clustering
- **Distance-based clustering** algorithm  
- **Optimal clusters** determined using:
  - **Elbow Method**
  - **Silhouette Score**
- **Cluster Labels Interpretation:**
  - `0` : Might Need Help  
  - `1` : Help Needed  
  - `2` : No Help Needed  

### DBSCAN Clustering
- **Density-based clustering** algorithm for handling nested clusters and outliers  
- **Hyperparameters:**  
  - `minPts`: Minimum points in neighborhood  
  - `epsilon`: Neighborhood radius  
- Useful for identifying outlier countries that do not clearly belong to any cluster  

### Agglomerative Hierarchical Clustering
- **Bottom-up hierarchical clustering**  
- Generates a **dendrogram** to visualize cluster merges  
- **3 final clusters selected** to categorize countries:  
  - `0` : No Help Needed  
  - `1` : Help Needed  
  - `2` : Might Need Help  

---

## Visualizations
- **Feature Distributions & Boxplots**  
- **Correlation Matrix**  
- **Scatterplots** for income vs. child mortality  
- **Dendrograms** for hierarchical clustering  
- **Cluster visualizations** after PCA transformation  

---

## Results & Insights
- Countries with **low income & high child mortality** are categorized as **high-priority for aid**  
- African nations dominate **high-risk clusters**  
- Wealthy countries (Singapore, Luxembourg, Qatar) cluster separately in **low-risk groups**  
- PCA allowed effective visualization while maintaining important variance  

---

## Tech Stack
- **Python**  
- **Pandas & NumPy** (data handling)  
- **Matplotlib & Seaborn** (visualization)  
- **Scikit-learn** (K-Means, DBSCAN, Hierarchical Clustering, PCA, Silhouette Score)  

---

## Setup & Installation

1. **Clone the repository**  
```bash
git clone https://github.com/GhadeerZahwe/Unsupervised-Learning-Fund-Allocation-For-Countries-in-Need.git
cd Unsupervised-Learning-Fund-Allocation-For-Countries-in-Need
```
2. **Create & activate virtual environment**
```bash
# Linux/Mac
python -m venv venv
source venv/bin/activate

# Windows (PowerShell)
python -m venv venv
.\venv\Scripts\activate
```
3. Install dependencies
```bash
pip install -r requirements.txt
```
