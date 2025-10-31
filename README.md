# Project Title: Digital Demand vs. Career Opportunities  
**Course:** DSA210 (2025-2026 Fall Term)  
**Student:** ANIL YOLCU  
**GitHub Link:** [https://github.com/anilyolcu/dsa210_project](https://github.com/anilyolcu/dsa210_project)

---

## 1. Motivation
Job searching and hiring are a key part of the economy. Traditional job market analysis often uses official statistics, but this data is frequently delayed.  
This project aims to explore a more modern, real-time approach. **Google Trends** can show public interest (acting as job "demand"), while **LinkedIn** reflects job "supply."

The main goal is to investigate whether a statistical relationship exists between these two digital data sources.  
If “what people are searching for” (Google) aligns with “what companies are offering” (LinkedIn), it may be possible to detect job market trends early.  
These insights could benefit both job seekers and companies.

---

## 2. Hypotheses

- **Null Hypothesis (H₀):**  
  There is no statistically significant relationship between the search volume of job-related keywords on Google and the number of corresponding job postings on LinkedIn across different occupations.

- **Alternative Hypothesis (H₁):**  
  There is a statistically significant relationship between the search volume of job-related keywords on Google and the number of corresponding job postings on LinkedIn across different occupations.

---

## 3. Datasets and Collection Plan

### *Primary Dataset: LinkedIn Job Postings*
- **Source:** [Kaggle - "LinkedIn Job Postings"](https://www.kaggle.com/datasets/arshkon/linkedin-job-postings)  
- **Content:** Over 3,000 job postings, including key features such as `job_title`, `location`, `posted_date`, and `job_description`.  
- **Collection Plan:** Downloaded directly from Kaggle as a `.csv` file.

### *Enrichment Dataset: Google Trends Search Volume*
- **Source:** [Google Trends](https://trends.google.com/trends/explore)  
- **Content:** Time-based interest data (scores from 0 to 100) for different job-related keywords.  
- **Collection Plan:**
  1. Analyze the `job_title` column from LinkedIn data to identify common job groups (e.g., "Data Scientist", "Software Engineer").  
  2. Use **Google Trends** to export monthly search data for these keywords.  
  3. Match time period and location with the LinkedIn dataset.

---

### *Merging Plan*
- Group LinkedIn data by **month** and **job group** (using `posted_date` and standardized titles).  
- Compute total **job_count** for each job per month.  
- Merge with Google Trends data (**search_volume**) using “Month/Year” and “Job Group” as keys.  

The resulting table will include:  
| Job Group | Month/Year | Job Count | Search Volume |
|------------|-------------|------------|----------------|
| Data Scientist | Jan 2023 | 250 | 85 |

---

## 4. Methodology and Analysis Plan

### *1. Data Preprocessing*
- Standardize job titles (e.g., “Sr. Data Scientist” → “Data Scientist”).  
- Convert `posted_date` to datetime format and extract month/year.  
- Handle missing values by dropping or imputing where necessary.

### *2. Exploratory Data Analysis (EDA) and Hypothesis Testing*
- Create **line plots** to visualize `job_count` and `search_volume` over time.  
- Perform **Pearson Correlation** analysis to test the strength of the relationship.  
- Use **scatter plots** to visualize correlation per job group.  
- Evaluate significance using **correlation coefficient (r)** and **p-value**.

### *3. Modeling (Later Stage)*
- If a significant correlation is found, build a **Simple Linear Regression** model:  
  - Input: `search_volume`  
  - Output: `job_count`

### *4. Evaluation*
- Statistical significance threshold: **p < 0.05**  
- Possible model evaluation metrics: **R²** and **Root Mean Square Error (RMSE)**.

---
