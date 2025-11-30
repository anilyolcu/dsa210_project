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

To make the analysis more focused, this project only considers **IT-related jobs**.  
These roles are closely connected to the internet and modern technologies, so it is more reasonable to expect an alignment between online search interest and the number of posted vacancies.

---

## 2. Hypotheses

- **Null Hypothesis (H₀):**  
  There is no statistically significant relationship between the Google search volume of IT job-related keywords and the number of corresponding IT job postings on LinkedIn across different IT role groups.

- **Alternative Hypothesis (H₁):**  
  There is a statistically significant relationship between the Google search volume of IT job-related keywords and the number of corresponding IT job postings on LinkedIn across different IT role groups.

---

## 3. Datasets and Collection Plan

### *Primary Dataset: LinkedIn Job Postings*
- **Source:** [Kaggle - "LinkedIn Job Postings"](https://www.kaggle.com/datasets/arshkon/linkedin-job-postings)  
- **Content:** Over 120,000 job postings, including key features such as `job_title`, `location`, `posted_date`, and `job_description`.  
- **Collection Plan:** Downloaded directly from Kaggle as a `.csv` file.
- **Data File:** The original raw LinkedIn dataset (`postings.csv`) is not included in this repository because of GitHub file size limits.  
You can download `postings.csv` from the Kaggle link given above and place it in the same folder as the notebook before running it.


### *Enrichment Dataset: Google Trends Search Volume*
- **Source:** [Google Trends](https://trends.google.com/trends/explore)  
- **Content:** Time-based interest data (scores from 0 to 100) for different job-related keywords.  
- **Collection Plan:**
  1. Analyze the `job_title` column from LinkedIn data to identify common job groups (e.g., "Data Scientist", "Software Engineer").  
  2. Use **Google Trends** to export total search data for these keywords within the corresponding time period.  

---

### *Merging Plan*
- Aggregate LinkedIn data by **IT role group** (using the standardized titles).  
- Compute the total **job_count** for each IT role group over the whole dataset.  
- Aggregate Google Trends data by the same **IT role group**, summing the **search_volume** for each role between **2023-01-01 and 2024-04-30**.  
- Merge the two aggregated tables using the IT role group name as the common key.

The resulting table includes one row per IT role group:

| IT Role Group      | Job Count (LinkedIn) | Search Volume |
|--------------------|----------------------|-------------- |
| Data Scientist     | 889                  | 2676          |


---

## 4. Methodology and Analysis Plan

### *1. Data Preprocessing*
- Load the Kaggle LinkedIn job postings dataset and keep only the **job title** column.  
- Clean and normalize titles (lowercase, remove extra symbols and spaces).  
- Map raw titles into around **20 standardized IT role groups** using a keyword-based dictionary  
  (e.g., “Sr. Data Scientist”, “Senior Data Science Specialist” → **“data scientist”** group).
- The keyword-based mapping rules for these IT role groups were initially drafted with the help of an LLM (ChatGPT) and then manually reviewed and adjusted by the author. 
- Drop rows that are marked as **non-IT / unknown**.  
- Count the number of postings for each IT role group and save this as `job_count`.  
- For the same 20 IT role groups, collect **Google Trends** data between **2023-01-01 and 2024-04-30** using consistent search terms.  
- Aggregate Google Trends interest over time for each role group to obtain a single **search_volume** value per IT role.

### *2. Exploratory Data Analysis (EDA) and Hypothesis Testing*
- Use **bar plots** to compare LinkedIn `job_count` and Google Trends `search_volume` across IT role groups.  
- Create **scatter plots**:
  - `job_count` vs `search_volume` (raw values),  
  - LinkedIn rank vs Google Trends rank for each IT role group.  
- Build a **rank comparison table** to see which roles have similar or different positions in both rankings.  
- Formally test the relationship between LinkedIn demand and Google search interest using  
  **Spearman rank correlation** (non-parametric, works on ranks and does not assume normality).  
- Evaluate significance using the **Spearman correlation coefficient (ρ)** and its **p-value**.

### *3. Modeling (Later Stage / Future Work)*
- If the relationship between `search_volume` and `job_count` is strong and consistent,  
  a simple **regression or ranking model** could be explored in a later phase,  
  where Google search interest is used as a predictor for job posting intensity by IT role group.

### *4. Evaluation*
- Statistical significance threshold: **α = 0.05** (we reject H₀ if p < 0.05).  
- Practical strength of the relationship is evaluated using the **size of Spearman ρ**  
  (e.g., weak, moderate, or strong positive association).  
- For any future prediction model, possible evaluation metrics could include **R²** and **Root Mean Square Error (RMSE)**.


---
