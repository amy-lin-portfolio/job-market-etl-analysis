# Job Market ETL & Data Analysis (Glassdoor Data Science Roles)

## Project Overview
This project builds a reproducible ETL and exploratory data analysis (EDA) pipeline to transform raw Glassdoor Data Science job postings into an analytics-ready dataset. The goal is to clean unstructured fields, engineer meaningful features, and analyze how skills, seniority, location, and industry sector relate to compensation.

The final output is a cleaned dataset suitable for analysis and a set of validated insights into job market trends.

---

## Dataset
- Source: Glassdoor Data Science job postings  
- Raw input file: `Uncleaned_DS_jobs.csv`  
- Records: ~670 job postings  
- Key fields include salary estimates, job descriptions, job titles, company names, locations, and industry metadata.

---

## ETL & Feature Engineering

### Salary Parsing
- Extracted minimum, maximum, and average salary values from unstructured salary text (e.g., "$137K–$171K (Glassdoor est.)")
- Removed annotations and converted salary ranges into numeric features:
  - `min_salary_k`
  - `max_salary_k`
  - `avg_salary_k`
- Validated salary distributions using summary statistics to ensure reasonable values.

---

### Company Name Cleaning
- Removed embedded company ratings from the `Company Name` field.
- Standardized names for readability and consistency.

---

### Location Standardization
- Parsed mixed location formats including:
  - City–state pairs (e.g., "Atlanta, GA")
  - State-only entries (e.g., "Texas")
  - Country-only entries (e.g., "United States")
  - Remote roles
- Engineered structured geographic features:
  - `city`
  - `state`
  - `is_remote`
  - `location_level` (city_state, state_only, country_only, remote, unknown)
- Preserved semantic meaning without introducing assumptions.

---

### Skill Extraction from Job Descriptions
- Extracted key technical skills from unstructured job descriptions using regex-based pattern matching.
- Created binary indicator columns (`req_<skill>`) for:
  - Python, SQL, Excel, Tableau, Power BI, R, AWS, Spark
- Used word boundary patterns to minimize false positives.
- Engineered a `skill_count` feature representing the breadth of technical requirements per role.

---

### Seniority Classification
- Standardized job titles into interpretable seniority categories using rule-based keyword matching:
  - Entry
  - Mid-Level
  - Senior
  - Lead/Manager
  - Unknown
- Prioritized leadership and senior individual contributor titles over experience-based wording.
- Interpreted Roman numerals (I, II) as role progression indicators.
- Preserved ambiguity where seniority could not be reliably inferred.

---

## Validation & Analysis
All analyses were validated using both **mean** and **count** to avoid misleading conclusions from small sample sizes.

Analyses included:
- Salary by individual technical skill
- Salary by remote vs in-person roles
- Salary by industry sector
- Salary by seniority
- Salary by number of required skills
- Interaction analysis between seniority and skill breadth

A single visualization was included to summarize average salary by seniority.

---

## Key Insights
- Leadership roles (Lead/Manager) exhibited the highest average salaries, highlighting the relationship between organizational responsibility and compensation.
- Individual technical skills (e.g., Power BI) were associated with only marginal salary differences, suggesting that single tools function as complementary requirements rather than primary drivers of pay.
- Remote roles showed average salaries comparable to in-person roles; however, the small number of fully remote postings limited the reliability of conclusions.
- Compensation varied meaningfully across sectors, with Government, Aerospace & Defense, and Business Services offering higher average salaries, while Insurance and Energy-related sectors trended lower.
- Salary did not increase linearly with the number of required skills. Roles requiring a moderate number of skills (approximately 3–5) tended to offer higher compensation.
- The relationship between number of skills and salary differed by seniority level, indicating that skills and seniority interact rather than independently determining compensation.

---

## Final Output
- Cleaned dataset exported as: `job_market_cleaned.csv`
- Notebook: `job_market_etl_analysis.ipynb`

---

## Tools & Technologies
- Python
- Pandas
- NumPy
- Regular Expressions (regex)
- Jupyter Notebook

---

## Notes
- This project emphasizes responsible data cleaning, validation, and interpretation. Results are descriptive and exploratory in nature and should be interpreted in the context of sample size limitations and job posting variability.
- Dropped columns that were not relevant to the analysis to improve readability and usability.

## Contact
For questions, please contact: jlin673@gatech.edu
