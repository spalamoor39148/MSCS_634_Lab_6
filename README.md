# MSCS_634_Lab_6

# Association Rule Mining Lab – Apriori vs FP-Growth

**Name:** Sri sai palamoor

**Course:** Advanced Big Data and Data Mining (MSCS-634-B01) 

**Lab Assignment:** Lab 6: Association Rule Mining with Apriori and FP-Growth

---

## Purpose of the Lab

The purpose of this lab is to understand and apply association rule mining techniques to extract meaningful patterns from real-world transactional data. Specifically, we employed the **Apriori** and **FP-Growth** algorithms to discover frequent itemsets and generate association rules that reveal relationships between purchased products.

Through this lab, we aimed to:

- Gain hands-on experience with data preprocessing and cleaning in Python.
- Understand the differences in performance and output between Apriori and FP-Growth.
- Use **Seaborn** and other visualization tools to explore patterns and interpret the results.
- Evaluate association rules based on **support**, **confidence**, and **lift**.
- Reflect on challenges encountered when working with a complex, messy retail dataset.

This work simulates a real-world use case in **market basket analysis**, frequently used in e-commerce, inventory planning, and product recommendations.

---

## Dataset Overview

We used the **Online Retail** dataset from the UCI Machine Learning Repository. This dataset contains over 500,000 records of transactions made between 2010 and 2011 by a UK-based online retailer. Each row represents a transaction and includes the following fields:

- InvoiceNo (Transaction ID)
- StockCode (Item Code)
- Description (Item Name)
- Quantity
- InvoiceDate
- UnitPrice
- CustomerID
- Country

The dataset required extensive cleaning before it was ready for mining.

---

## Step-by-Step Process

### 1. Data Cleaning & Preprocessing

- Removed canceled transactions (Invoice numbers starting with 'C').
- Dropped rows with missing values (especially `CustomerID` and `Description`).
- Filtered for transactions from the **United Kingdom** only to reduce noise and focus the analysis.
- Stripped and standardized item descriptions to avoid duplication due to text inconsistencies.
- Grouped data by `InvoiceNo` and created a **basket matrix** for market basket analysis.

### 2. Exploratory Data Analysis

- Created a **barplot** of the most frequently purchased items.
- Generated a **Seaborn heatmap** to show co-occurrences of top items.
- Identified which items often appear together in customer baskets.

### 3. Apriori Algorithm

- Used `mlxtend`'s `apriori` function with `min_support=0.01`.
- Generated association rules using `min_confidence=0.3` and analyzed rules based on **lift**.
- Visualized rules via scatterplots (support vs. confidence) and top itemsets.

### 4. FP-Growth Algorithm

- Applied `fpgrowth()` with the same minimum support as Apriori.
- Compared rule generation time and rule quality.
- Observed similar but more numerous itemsets in less time.

---

## Key Insights from Analysis

### Frequent Items

- **Top-selling items** included:
  - *White Hanging Heart T-Light Holder*
  - *Regency Cakestand 3 Tier*
  - *Jumbo Bag Red Retrospot*

- Items frequently co-purchased were often within the same category (e.g., decorative or home-related).

### Sample Strong Association Rule

> **{REGENCY CAKESTAND 3 TIER} → {PARTY BUNTING}**  
> - **Support:** 0.016  
> - **Confidence:** 0.902  
> - **Lift:** 6.92  

This indicates that nearly 90% of the time someone buys the cakestand, they also purchase bunting—suggesting a strong bundling opportunity for promotions.

---

## Comparative Analysis

### Algorithm Performance

| Metric             | Apriori          | FP-Growth        |
|--------------------|------------------|------------------|
| Execution Time     | Slower (several seconds) | Faster (under a second) |
| Memory Usage       | Higher            | Lower             |
| Rule Coverage      | Broad             | Slightly broader  |
| Scalability        | Limited on large data | Efficient         |

- **FP-Growth** was significantly faster and more scalable than Apriori, especially for datasets with large numbers of items.
- Both algorithms produced similar high-quality rules with comparable support and confidence.
- FP-Growth worked better with sparse data due to its efficient FP-tree structure.

---

##  Challenges & Resolutions

| Challenge | Description | Resolution |
|----------|-------------|------------|
| Canceled Orders | Transactions with negative quantities or InvoiceNo starting with "C" | Filtered them out |
| Missing Values | Nulls in `CustomerID` or `Description` | Removed null rows |
| Long Processing Time | Apriori was slow on full dataset | Increased `min_support` and filtered by UK |
| Text Inconsistencies | Item names had leading/trailing spaces or inconsistent cases | Cleaned using `.str.strip().str.lower()` |
| Too Many Rules | At low confidence, rule count exploded | Set `min_confidence = 0.3` for clarity |
| Overcrowded Visuals | Too many bars/labels in plots | Plotted top 10–20 items or rules only |

---

## Takeaways

- Association Rule Mining is a powerful unsupervised learning technique that can reveal **hidden relationships** in customer purchasing behavior.
- **FP-Growth** outperforms **Apriori** in terms of speed and scalability, especially when dealing with large or sparse datasets.
- **Visualizations** like heatmaps, bar charts, and scatter plots enhance interpretability and presentation of results.
- This lab reinforces the importance of **data preprocessing**, **parameter tuning**, and **critical interpretation** in data science workflows.

---

## Files Provided

- `Online Retail.xlsx` – Source dataset

---

