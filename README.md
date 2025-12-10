# Startup-Corporate Partnership Selection with Logistic Regression

This project builds a simple, interpretable machine learning pipeline to help companies identify high-potential startup partners using only publicly available data on German digital tech startups.

The project is part of a research collaboration on startup-corporate partnerships and has been:

- Presented at **2025 IEEE ETECOM25 Conference**, Track “Artificial Intelligence, Machine Learning, and Business Analytics”.
- Submitted to **Data Science in Finance and Economics (DSFE)** (final stage of peer review).

---

## Project Highlights

- Cut data collection and cleaning time by approximately **30-40%** by building web-scraping workflows, turning a multi-week manual task into a repeatable pipeline.  
- Improved data quality and consistency across sources, reducing mismatched or conflicting records by approximately **25%** through standardized industry tags, funding stages, hub names, and country labels.  
- Trained an interpretable **Logistic Regression** model that reached **88.2% accuracy**, **0.80 precision**, and an **F1-score of 0.727** on the balanced dataset.  

---

## Motivation

Traditional methods for identifying strategic partners often rely on human judgment and informal networks. This can lead to:

- Biased selection criteria  
- Missed opportunities outside existing networks  
- Slow, manual screening when the candidate pool is large  

This project aims to:

> Provide a replicable, data-driven framework that supports early partner screening using public startup data, while remaining simple enough to interpret and deploy in SMEs.

---

## Dataset Overview and EDA

The dataset focuses on Germany’s digital tech startup landscape:

- **755 startups**  
- **53** labeled as “high-potential partners” by the focal company (heavily imbalanced target)  

Data was collected from:

- Public startup and ecosystem databases  
- German digital hub websites  
- Company and startup pages  

### Exploratory Data Analysis (EDA)

- **1. Descriptive characteristics**
  - SaaS dominates the sample industries, with 300+ SaaS startups (nearly half), alongside high proportions of AI and Data Analytics.
  - 96.7% of firms are very small (fewer than 50 employees), and around 40% are in pre-seed or seed funding stages.
  - Despite their early-stage profile, about 82% of startups explicitly state that they are actively looking for partners rather than prioritising funding (which was often more significant for startups), highlighting the importance of strategic alliances.
  - Only 9.8% (74 out of 755) of startups have at least one female founder, showing a pronounced gender imbalance in leadership.
  - Only 53 startups are labeled as “high-potential” by the focal company, underscoring the strong class imbalance in the target variable.

- **2 – Hub affiliations of startups**
  - Hub Frankfurt/Darmstadt hosts the largest number of startups (140+), reflecting its role as a major financial, educational, and innovation centre.

- **3. Geographic distribution and hubs**
  - Maps the spatial distribution of startups and their associated hubs across Germany.
  - Startups tend to cluster around key hubs, suggesting that government-backed digital hubs and ecosystems play a significant role in boosting entrepreneurial activity.

---

## Methods Overview

### 1. Data Collection and Cleaning

- Automated web scraping of startup and hub information.  
- Removal of duplicates and inconsistent entries.  
- Standardization of:
  - Industry and technology tags  
  - Funding stages  
  - Hub names and regions  
  - Country and location labels  

This step significantly reduced manual workload and made updates to the dataset repeatable.

### 2. Feature Engineering

Key feature groups:

- **Technology focus**  
  - e.g., indicators for IoT/Smart Systems, AI/Data Analytics  
- **Funding stage**  
  - Pre-seed, seed, early, later-stage funding  
- **Geographic distance**  
  - Approximate distance between startup and focal company
- **Business model**  
  - B2B vs B2C vs Both
- **Hub affiliation**  
  - Membership in Germany’s digital innovation hubs  
- **Founders’ structure**  
  - Including percentage of female vs male founders  

### 3. Labeling and Imbalance Handling

- Positive class: startups previously selected as “high-potential” partners by the company.  
- Negative class: dictated using heuristic clustering on unselected startups.  
- Applied **SMOTE** to oversample the minority class and mitigate class imbalance.

### 4. Model

- Binary classification with **Logistic Regression** to keep the model interpretable.  
- Evaluation metrics:
  - Accuracy  
  - Precision  
  - Recall  
  - F1-score  

Final model performance on the balanced dataset:

- Accuracy: **88.2%**  
- Precision: **0.80**  
- F1-score: **0.727**  

---

## Key Insights - Key Drivers

### 1. Technology Prowess 

Features capturing technology focus (especially IoT/Smart Systems and AI/Data Analytics) have the highest odds ratios in the logistic regression model.

- Startups with strong emphasis on **IoT and Smart Systems** can be nearly **20 times** more likely to be classified as high-potential.  
- AI and Data Analytics-focused startups show an even stronger increase in odds.

**Interpretation:**  
Technological capabilities are central to how this company screens partners. While the specific technologies of interest will vary by company and sector, the overarching pattern is that deep tech expertise is a core signal of “high-potential” partners.

---

### 2. Funding Stage 

The funding stage variable is positive and significant:

- Later-stage startups are several times more likely to be classified as high-potential than those in pre-seed or seed.  
- Within the earliest phases (pre-seed, seed), only about **23-26%** of startups are labeled high-potential (after resampling).  
- For later funding stages, this proportion at least doubles.

**Interpretation:**  
The company places clear emphasis on financial maturity and prior validation. In high-risk, high-tech domains, this helps mitigate the risk associated with very early-stage ventures.

---

### 3. Geographic Proximity

Distance between the startup and the focal company has a strong negative effect:

- Increasing distance sharply reduces the probability of being classified as high-potential.  
- Beyond roughly **200 km**, only about **6-7%** of startups are selected as suitable candidates.  
- When mapped, most promising startups cluster within approximately 200 km of the focal company and are predominantly located within Germany.

**Interpretation:**  
Despite the digital nature of the industry, physical proximity remains important. Possible reasons include lower coordination and travel costs, fewer communication barriers, and a tendency toward “local search bias”.

---

### 4. Business Model Fit 

The business model variable (B2B vs B2C) is also significant:

- B2B startups are markedly more likely to be identified as high-potential partners.  
- The company in this case clearly favors B2B offerings over B2C.

**Interpretation:**  
Customer-type alignment is a key part of early screening. Even a strong technology fit may not be enough if the business model does not match the corporate partner’s strategic goals.

---

### 5. Gender of Founders is Not a Decisive Factor 

- The percentage of female founders shows strong association with the target variable when considered alone.  
- However, once other variables (technology, funding, geography, business model) are included, its effect is no longer statistically significant.

**Interpretation:**  
In this specific study, gender composition does not independently drive selection once core strategic and other factors are taken into account, even though male leaders dominate the market.

---

### 6. Hubs and Ecosystems Have Indirect Advantages

- Hubs like Frankfurt/Darmstadt host large concentrations of startups and act as important innovation centers.  
- The Karlsruhe AI hub shows a large coefficient but becomes statistically unstable once direct technology features are added.

**Interpretation:**  
Being part of an innovation hub may indirectly improve partnership potential through better resources, talent access, and visibility, but much of this effect is captured by explicit technology-related features in the model.

---

## Practical Implications

For startups:

- Emphasize key technologies that align with potential partners’ needs (such as IoT, AI, or Data Analytics in this case).  
- Make funding stage and financial stability easy to understand.  
- Clarify business model fit (e.g., B2B vs B2C) when approaching corporate partners.  
- Prioritize reaching to corporates within a reasonable geographic radius.

For companies and SMEs:

- A straightforward Logistic Regression model on public data can significantly improve early-stage screening.  
- The framework can:
  - Identify which criteria truly shape past decisions.  
  - Produce a ranked list of candidates with selection probabilities.  
  - Reduce reliance on unstructured networks and ad-hoc impressions.
