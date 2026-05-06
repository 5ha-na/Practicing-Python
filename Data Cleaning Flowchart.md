# Python Data Cleaning Process
Added a flowchart and step-by-step guide for the Python data cleaning process using Pandas.

```mermaid
flowchart TD
    Start[Raw DataFrame] --> A[Inspect Data]
    A --> B[Check Missing Values]
    B --> C{Handle Missing Values}
    
    C -->|Drop rows| D[Drop NA]
    C -->|Fill constant| E[Fill with value]
    C -->|Forward fill| F[Forward fill]
    C -->|Interpolate| G[Interpolate]
    C -->|Fill mean| H[Fill with average]
    
    D --> I[Remove Duplicates]
    E --> I
    F --> I
    G --> I
    H --> I
    
    I --> J[Standardize Text]
    J --> K[Fix Data Types]
    K --> L[Handle Outliers]
    L --> M[Feature Engineering]
    M --> N[Encode Categoricals]
    N --> O[Scale or Normalize]
    O --> P[Save Cleaned Data]
    P --> End[Clean DataFrame Ready]
```
| Step | Python Pandas Code |
|------|---------------------|
| **1. Inspect Data** | `df.info()`<br>`df.head()`<br>`df.describe()` |
| **2. Check Missing Values** | `df.isnull().sum()` |
| **3. Drop rows with NA** | `df.dropna()` |
| **4. Fill with constant** | `df.fillna('Unknown')` |
| **5. Forward fill** | `df.fillna(method='ffill')` |
| **6. Interpolate** | `df.interpolate()` |
| **7. Fill with mean/median** | `df.fillna(df['col'].mean())` |
| **8. Remove Duplicates** | `df.drop_duplicates()` |
| **9. Standardize Text** | `df['col'] = df['col'].str.strip().str.upper()` |
| **10. Fix Data Types** | `df['date'] = pd.to_datetime(df['date'])`<br>`df['value'] = pd.to_numeric(df['value'])` |
| **11. Handle Outliers (IQR)** | `Q1 = df['col'].quantile(0.25)`<br>`Q3 = df['col'].quantile(0.75)`<br>`IQR = Q3 - Q1`<br>`df = df[(df['col'] >= Q1 - 1.5*IQR) & (df['col'] <= Q3 + 1.5*IQR)]` |
| **12. Feature Engineering** | `df['age_group'] = pd.cut(df['age'], bins=[0,18,60,100], labels=['child','adult','senior'])` |
| **13. Encode Categoricals** | `df = pd.get_dummies(df, columns=['category'])` |
| **14. Scale or Normalize** | `from sklearn.preprocessing import StandardScaler`<br>`scaler = StandardScaler()`<br>`df[['col']] = scaler.fit_transform(df[['col']])` |
| **15. Save Cleaned Data** | `df.to_csv('cleaned_data.csv', index=False)` |
