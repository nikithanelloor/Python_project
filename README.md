## Google Play App Rating Prediction

**Objective:** Predict future app ratings using pre-launch app metadata to help identify high-potential apps for visibility boost.

---

## Problem Statement
Google Play is planning a feature to promote promising apps by boosting their visibility. To qualify for promotion, apps ideally should have high user ratings.  
**Task:** Develop a model that predicts an app’s likely rating based on metadata, enabling early identification of high-potential apps.

---

## Dataset Overview
(`googleplaystore.csv`)

| Field              | Description                                    |
|-------------------|------------------------------------------------|
| App               | Name of the application                        |
| Category          | Primary category                               |
| Rating            | App’s average user rating (target variable)    |
| Reviews           | Number of user reviews                         |
| Size              | App size                                       |
| Installs          | Number of installs                             |
| Type              | Paid or Free                                   |
| Price             | Price of the app                               |
| Content Rating    | Targeted age group                             |
| Genres            | One or more genres                             |
| Last Updated      | Date of last update                            |
| Current Ver       | App version                                    |
| Android Ver       | Minimum required Android version               |

## Methodology
### Data Loading
Loaded data using Pandas:Organized into a clear data

### Data Cleaning & Preprocessing
Removed missing values in any column (df.dropna()).
**Normalized formats:**
- Size: extracted numeric values, converted Mb → Kb.
- Reviews, Installs, and Price: stripped symbols (+,, $) and converted to numeric types.
**Ensured sanity:**
- Ratings restricted to [1, 5];
- Dropped records where reviews exceed installs;
- Excluded free apps erroneously priced > $0.
These steps ensured reliable, consistent metrics 

### Exploratory Analysis & Outlier Treatment
- Created boxplots (Price, Reviews) and histograms (Rating, Size) to inspect distributions.

**Identified and removed extreme outliers:**

- Apps priced > $200

- Reviews > 2 million

- Installs beyond a selected percentile threshold
This reduced skew and improved model interpretability .

### Bivariate Analysis
Analyzed relationships between Rating and:

- Numeric features via scatter/join plots (Price, Size, Reviews)

- Categorical traits via boxplots (Category, Content Rating)

- Documented findings to inform feature selection and engineering 

### Feature Engineering
- Transformed heavy-tailed numeric variables (Reviews, Installs) to stabilize variance.

- One-hot encoded categorical features (Category, Genres, Content Ratings).

- Dropped irrelevant metadata (App name, version info) to reduce noise .

### Model Development
- Split the data into training and testing sets (70:30 ratio).

- Built a Linear Regression model.

- Measured performance using R² on both training and test sets to assess generalization ability.

- Evaluated and documented model assumptions and limitations.

 ## Insights
- Freemium dominance: The thin line at zero in the price distribution confirms most apps are free. A few outliers above $300 are likely a typical or junk apps. 


- Rating concentration: Most app ratings fall between 3.5 and 4.8, indicating generally strong user satisfaction.

- App size insights: The majority of apps are under 30 MB, but some go up to ~100 MB. The average Play app size is about 11–17 MB—confirming your distribution.

- Price vs. Rating: Scatter plots show high ratings even for free apps, confirming that paying more doesn't guarantee better ratings—quality and UX matter more. 

- Size vs. Rating: No clear pattern—small and large apps can both achieve high ratings. 

- Content Rating patterns: ‘Adult Only 18+’ apps show consistently high ratings with low spread; other groups hover around 4.0–4.5, indicating reliable quality. 

- Model generalization: Similar shapes in training and testing Actual vs. Predicted plots show consistent performance. Results:

     Training MSE: 0.25; Testing MSE: 0.27

     Training R²: 0.15; Testing R²: 0.14

## Conclusions
- Despite being free, most apps achieve high ratings, reaffirming the dominance of freemium models.

- Good quality,UX, features, and user satisfaction drive ratings—not price or file size.

- Specific content ratings and genres (Adult, Entertainment) consistently receive high user approval.

- The moderate R² and close MSE values suggest linear model is stable.

## Recommendations
-  Maintain free app access, supplementing revenue via in-app strategies (ads, premium features).

- Focus on UX and feature quality: Prioritize user experience improvements over increasing app size or price.

- Target high-performing content segments: Develop for genres like Entertainment and Adult programs to maximize positive reception.

- Enhance predictive models: Integrate sentiment analysis, retention data, and update frequency to improve R².

- Explore advanced models: Consider gradient boosting or random forests for better fit.

- Implement ongoing monitoring: Track model performance over time and retrain as reviews and market behavior evolve. 
