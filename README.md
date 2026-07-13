# Mall Customer Segmentation using K-Means Clustering

## 1) Task Objective

The objective of this project is to segment mall customers into meaningful groups using unsupervised machine learning so that marketing efforts can be personalized and budget can be allocated more effectively.

Given the dataset fields:

- `CustomerID`
- `Genre`
- `Age`
- `Annual Income (k$)`
- `Spending Score (1-100)`

the main goal is to identify distinct customer clusters based primarily on behavioral purchasing patterns, and then translate those clusters into actionable business strategies.

In short, this project answers:

- **Who are the high-value customers?**
- **Which customers need engagement campaigns?**
- **How can promotions be targeted by segment instead of using one generic strategy?**

---

## 2) My Approach

### A. Data Understanding and Preparation

- Loaded `Mall_Customers.csv` (200 rows, 5 columns).
- Verified structure, data types, and summary statistics.
- Checked data quality:
  - Missing values: **none**
  - Duplicate rows: **none**
- Dropped `CustomerID` for modeling (identifier only, no clustering value).
- Encoded `Genre` into numeric form for analysis support (`Genre_Encoded`), while keeping gender mainly for profiling.
- Renamed columns for cleaner coding:
  - `Annual Income (k$)` → `Annual_Income`
  - `Spending Score (1-100)` → `Spending_Score`

### B. Exploratory Data Analysis (EDA)

Performed visual and statistical EDA to understand customer behavior:

- Gender distribution
- Histograms for `Age`, `Annual_Income`, `Spending_Score`
- Boxplots by gender
- Pairplot for feature relationships
- Correlation heatmap
- Core business scatter plot: `Annual_Income` vs `Spending_Score`

Key EDA observation:
- Income and spending do not show strong linear correlation, but visually form cluster-like groupings (ideal for K-Means).
- Gender did not show strong separation in spending behavior.

### C. Feature Strategy and Scaling

Built two feature sets:

1. **Primary (used for core clustering):**
   - `Annual_Income`, `Spending_Score`
2. **Extended (used for comparison/visual exploration):**
   - `Age`, `Annual_Income`, `Spending_Score`

Applied **StandardScaler** to avoid scale dominance in Euclidean-distance-based K-Means.

### D. Model Building and Cluster Selection

Used K-Means and evaluated multiple values of `k` (2 to 10) with:

- **Elbow Method (WCSS/Inertia)**
- **Silhouette Score**
- **Davies-Bouldin Index**

From your notebook outputs:

- Best Silhouette Score occurs at **k = 5** (`~0.5547`)
- Lowest Davies-Bouldin Index also at **k = 5** (`~0.5722`)

So the final model uses **5 clusters**.

### E. Cluster Visualization and Profiling

- Visualized final clusters in 2D (`Income` vs `Spending`).
- Used dimensionality reduction (PCA / t-SNE) for additional cluster structure visualization.
- Profiled clusters by average demographic and spending behavior.
- Interpreted each cluster into business-facing customer personas.

---

## 3) Results and Insights

### Model Outcome

- Final segmentation: **5 customer clusters**
- Validation metrics support this choice:
  - Silhouette peaked at `k=5`
  - Davies-Bouldin minimized at `k=5`
- Clusters are well-separated and business-interpretable.

### Business Insights (Segment-Level)

From the clustering pattern, customer groups generally map to common retail segments:

1. **High Income, High Spending**
   - Premium/high-value customers  
   - Strategy: loyalty rewards, VIP events, exclusive early-access offers

2. **High Income, Low Spending**
   - Affluent but under-engaged customers  
   - Strategy: personalized recommendations, premium product discovery campaigns

3. **Low Income, High Spending**
   - Highly engaged value-seeking shoppers  
   - Strategy: bundle deals, limited-time offers, retention incentives

4. **Low Income, Low Spending**
   - Low engagement customers  
   - Strategy: awareness campaigns, entry-level promotions, conversion-focused outreach

5. **Mid Income, Mid Spending (Balanced Segment)**
   - Stable mainstream customer base  
   - Strategy: broad seasonal campaigns, cross-sell/upsell, consistency-focused retention

### Overall Conclusion

This project demonstrates that unsupervised learning can convert raw customer data into actionable segments for targeted marketing.  
Using K-Means with proper scaling and cluster validation provides a practical, interpretable framework for customer strategy design in real business settings.
