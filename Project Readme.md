# **📊 Personal Finance Data Analytics & Dashboard**

## **📖 Project Overview**

This project provides an end-to-end data analytics, statistical analysis, and business intelligence solution for personal finance and expense tracking. Raw transaction logs are processed through a data cleaning and feature engineering pipeline in **Python**, evaluated via **Exploratory Data Analysis (EDA)** and **Inferential Statistics (Hypothesis Testing)** in **Jupyter Notebooks**, and modeled into an interactive **Power BI** executive dashboard (.pbix).

## **🎯 Project Objectives**

The primary objective of this project is to audit personal expenditure, identify spending patterns, identify high-value transactions and spending spikes, and uncover statistical drivers behind spending habits. Specifically, the project aims to:

* **Cleanse & Normalize Data:** Remove duplicates, drop invariant attributes, validate transaction bounds, and cast temporal fields.  
* **Engineer Temporal Dimensions:** Extract month, weekday, and weekend classifications to evaluate cyclical spending behaviors.  
* **Track Core Financial KPIs:** Measure total expenditure, average ticket size, transaction volume, median expense, and maximum outflow.  
* **Conduct Statistical Hypothesis Testing:** Test for significant differences between weekday and weekend spending (![][image1]\-test), check distribution normality (Shapiro-Wilk), and compute a 95% confidence interval for mean transaction amounts.  
* **Build Business Intelligence Reports:** Deliver interactive category breakdowns, temporal heatmaps, and multi-parameter slicers in Power BI.

## **🛠️ Tools & Technologies Used**

* **Python 3.10+:** Core programming language for data manipulation and numerical computation.  
* **Pandas & NumPy:** Data cleaning, deduplication, datetime parsing, and feature engineering.  
* **SciPy (scipy.stats):** Two-sample independent ![][image1]\-test, Shapiro-Wilk normality test, and confidence interval estimation.  
* **Matplotlib & Seaborn:** Data visualization, KDE distribution plots, category bar charts, and cross-dimensional heatmaps.  
* **Power BI Desktop:** Semantic data modeling, DAX measures, KPI cards, and interactive dashboard visuals.  
* **Jupyter Notebook:** Interactive environment for pipeline development and documentation.

## **📈 Key Performance Indicators (KPIs)**

Based on the cleaned dataset of **793 cleaned transactions**, the following core financial metrics are tracked:

* **Total Spending:** ![][image2] (Overall expenditure across all categories).  
* **Average Transaction Size:** ![][image3] (Mean expense per transaction).  
* **Median Transaction:** ![][image4] (Reflects typical high-frequency daily expenses).  
* **Total Transactions:** ![][image5] (Cleaned from 938 raw records; 145 duplicates removed).  
* **Maximum Outlier Transaction:** ![][image6] (Single largest capital outflow).  
* **95% Confidence Interval (Mean):** ![][image7] (Estimated true population mean range).

## **🎨 Dashboard Architecture & Features**

The Power BI dashboard model (dashboard.pbix) organizes insights into interactive analytical views:

1. **Executive KPI Cards:** Immediate visibility into *Total Outflow*, *Average Ticket Size*, *Median Expense*, and *Transaction Count*.  
2. **Category-wise Spending Breakdown:** Horizontal ranking visual of all 14 expense categories to distinguish major vs. discretionary allocations.  
3. **Monthly Outflow Trajectory:** Time-series line chart tracking monthly spend from January to December, highlighting annual peaks and troughs.  
4. **Weekday vs. Weekend Spending Analysis:** Comparative bar charts evaluating total expenditure volume versus average spend per transaction.  
5. **Day of Week ![][image8] Month Heatmap:** Matrix visualization identifying exact calendar periods and weekdays with concentrated spending spikes.  
6. **Multi-Attribute Slicers:** Dynamic filtering across *Month*, *Day of Week*, *Is\_Weekend*, *Category*, and *Account*.

## **🧹 Data Cleaning & Preprocessing Pipeline**

Executed in data\_cleaning.ipynb:

* **Initial Data Audit:** Ingested 938 raw records across 6 columns (date\_time, category, account, amount, currency, tags).  
* **Deduplication:** Identified and eliminated **145 redundant records** via df.drop\_duplicates(inplace=True), yielding a clean base of **793 entries**.  
* **Invariant Feature Removal:** Dropped the currency column as it contained a single uniform value (BYN).  
* **Datetime Transformation:** Converted date\_time object strings to native pandas datetime64\[ns\] timestamps.  
* **Feature Engineering:**  
  * Month: Extracted calendar month name (e.g., *January*, *March*, *November*).  
  * Day\_of\_Week: Extracted day name (e.g., *Monday*, *Wednesday*).  
  * Is\_Weekend: Created a boolean flag (dt.dayofweek \>= 5\) isolating Saturdays and Sundays.  
* **Constraint Validation:** Verified absence of negative values (df\[df\["amount"\] \< 0\] returned 0 rows).  
* **Export:** Serialized the processed dataset to Expenses\_Final.csv.

## **🔬 Statistical Analysis & Hypothesis Testing**

Executed in eda.ipynb using scipy.stats:

| Statistical Test / Metric | Methodology | Result | Inference & Conclusion |
| :---- | :---- | :---- | :---- |
| **Two-Sample Independent t-Test** (Weekday vs. Weekend) | Compares mean transaction amounts across weekday and weekend groups | **t = 0.36, p = 0.7162** | **p > 0.05 — Fail to reject H₀.** There is no statistically significant difference in average transaction size between weekdays (**19.07 BYN**) and weekends (**16.30 BYN**). |
| **Normality Assessment** (Shapiro-Wilk Test) | Tests whether expenditure follows a Gaussian distribution | **W = 0.1634, p < 0.001** | **p < 0.05 — Reject normality.** Spending is heavily right-skewed with high frequency of low-ticket transactions and occasional large capital transfers. |
| **95% Confidence Interval** | Student's t-distribution on sample mean | **[12.61, 24.45] BYN** | The 95% confidence interval for the estimated mean transaction amount is **12.61–24.45 BYN**. |


## **💡 Key Insights**

* **Capital vs. Daily Expense Distribution:**  
  * Top capital categories Loan given (![][image19]) and Other (![][image20]) represent **\~37.5%** of all expenditures.  
  * Routine living expenses like Food (![][image21]), Cafe (![][image22]), and Public transport (![][image23]) generate high transaction volume with a low median cost of ![][image4].  
* **Monthly Outflow Cycles:**  
  * **March** was the peak spending month of the year, driven by high-value transfers (![][image6] loan and ![][image24] other expense on March 5).  
  * **September** formed the second major spending wave (![][image25] purchase on September 29).  
  * **February** and **May** recorded the lowest overall spending.  
* **Day-of-Week Patterns:**  
  * **Wednesday** accumulated the highest total spending (![][image26]), followed by **Monday** (![][image27]) and **Thursday** (![][image28]).  
  * Weekdays accounted for **82.8%** of total spending (![][image29]) versus weekends (![][image30]), primarily driven by 4.8x higher transaction frequency rather than larger individual purchase sizes.


## **📁 Repository Structure**

├── data_cleaning.ipynb            # Data cleaning, deduplication & feature engineering
├── eda.ipynb                      # Exploratory data analysis & hypothesis testing
├── Expenses_Clean_Final.csv       # Final cleaned, engineered dataset
├── dashboard.pbix                 # Interactive Power BI report & data model
└── README.md                      # Comprehensive project documentation
