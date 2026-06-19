# 2026 AI Job Market Analysis

This project analyzes a dataset of AI-related job postings across multiple countries to better understand the structure of the AI job market.

The goal is to explore:

* Which AI job categories appear most often
* Which skills are most frequently requested
* How salary data varies across roles and countries
* How complete the original skill data was
* How skill coverage can be improved using a data pipeline
* Whether machine learning models can learn useful patterns from job postings

This is a portfolio project focused on data cleaning, exploratory data analysis, skill extraction, visualization, and introductory machine learning.

---

## Project Overview

The project is divided into three main notebooks:

| Notebook                                                | Purpose                                                                                                                                          |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `01_build_skill_dataset.ipynb`                          | Cleans the raw dataset, normalizes job titles, maps roles to ESCO occupations, completes missing skills, and creates the final analysis dataset. |
| `02_job_market_insights.ipynb`                          | Performs exploratory data analysis and creates market insight visualizations.                                                                    |
| `03_machine_learning_analysis_ai_job_market_data.ipynb` | Applies machine learning models for salary analysis, salary band classification, job category classification, skill prediction, and clustering.  |

---

## Dataset Summary

The final dataset contains:

* 5,773 AI-related job postings
* 5 countries
* 16 normalized job categories
* Salary information when available
* Original skills when provided
* Recommended skills generated from the skill completion pipeline
* Job descriptions, titles, companies, experience levels, and remote status

The original dataset had limited skill coverage. Only a small portion of job postings included explicit required skills.

To improve the analysis, this project builds a skill enrichment pipeline that combines:

1. Original skills when available
2. Job title normalization
3. ESCO occupation mapping
4. KNN-based skill inference
5. Local LLM validation with Ollama
6. Rule-based rescue for obvious skills removed too aggressively
7. Final recommended skill selection

---

## Main Results

### Dataset Coverage

The final dataset has much better skill coverage after enrichment.

![Dataset Coverage](outputs/figures/coverage_by_field.png)

Key observations:

* Salary data is available for a meaningful portion of the dataset, but not for every country equally.
* Original skill coverage was low.
* Recommended skill coverage is much higher after the skill completion pipeline.
* Salary analysis should be interpreted carefully because salary availability varies by country.

---

## Job Market Distribution

### Job Postings by Country

![Job Postings by Country](outputs/figures/job_postings_by_country.png)

The dataset covers job postings from the United States, United Kingdom, Canada, Germany, and Australia.

The distribution is not perfectly balanced, so country-level results should be interpreted with sample size in mind.

---

### Top Job Categories

![Top Job Categories](outputs/figures/top_job_categories.png)

The largest job categories include:

* AI Engineer
* Data Scientist
* Machine Learning Engineer
* Software Engineer
* LLM Engineer
* Research Scientist
* MLOps Engineer

The market is concentrated around a few major role families.

---

## Skill Demand Analysis

### Top Recommended Skills

![Top Recommended Skills](outputs/figures/top_recommended_skills.png)

The most common skills include general programming, AI, NLP, cloud, and generative AI related technologies.

The final recommended skills should be interpreted as enriched market signals. They are not always skills explicitly written by employers in the original job postings.

---

## Salary Analysis

Salary analysis is performed carefully because salary data is incomplete and salaries across countries should not be compared directly without currency normalization.

For this reason, some salary modeling focuses on United States postings only.

### US Salary Distribution

![US Salary Distribution](outputs/figures/salary_distribution_us.png)

Salary distributions are noisy and contain outliers, so median values and salary bands are often more reliable than simple averages.

---

### US Salary by Experience Level

![US Salary by Experience Level](outputs/figures/salary_by_experience_level_us.png)

Experience-level salary patterns should be interpreted carefully. Some groups can have small sample sizes or unusual role mixes.

For example, junior roles may sometimes appear to have unexpectedly high salaries if they are concentrated in specialized AI, ML, or PhD-level postings.

---

## Machine Learning Analysis

The machine learning notebook explores whether job market patterns can be learned from the dataset.

The project includes:

* Baseline salary prediction
* Linear regression
* Random Forest regression
* Salary band classification
* Job category classification from text
* Multi-label skill prediction
* Job clustering and market segmentation

The goal is not to create a production-level model. The goal is to evaluate whether the dataset contains learnable structure and to explain the limitations clearly.

---

### Job Clustering

![Job Clusters](outputs/figures/job_clusters_2d.png)

Clustering is used to group similar job postings based on text and skill information.

The clusters help identify broad job market segments such as:

* AI / GenAI roles
* Data science roles
* Machine learning engineering roles
* MLOps / cloud roles
* Software and platform engineering roles

---

### Salary Model Feature Importance

![Random Forest Salary Feature Importance](outputs/figures/rf_salary_feature_importance.png)

Feature importance gives a rough view of which variables helped the model predict salary.

These results should not be interpreted as causal. They only show which features were useful for prediction in this dataset.

---

### Job Category Classification

![Job Category Confusion Matrix](outputs/figures/job_category_confusion_matrix.png)

The job category classifier tests whether normalized job categories can be learned from job titles and descriptions.

Classification errors are useful because they reveal ambiguous roles and overlapping job families.

---

### Salary Band Classification

![Salary Band Confusion Matrix](outputs/figures/salary_band_confusion_matrix_rf.png)

Salary band classification can be more stable than predicting exact salaries because job posting salaries are noisy and can contain outliers.

---

## Methods Used

### Data Cleaning

* Removed duplicate rows
* Standardized text fields
* Cleaned city names
* Converted posting dates
* Detected truncated job descriptions
* Cleaned German and French job titles
* Created analysis-ready helper columns

### Job Title Normalization

Job titles were mapped into a custom taxonomy of 16 categories:

* AI Engineer
* Machine Learning Engineer
* Data Scientist
* Data Engineer
* Research Scientist
* Computer Vision Engineer
* NLP Engineer
* LLM Engineer
* MLOps Engineer
* DevOps Engineer
* Platform Engineer
* Software Engineer
* Solutions Architect
* Product / Management
* Consultant
* Other

### Skill Completion Pipeline

The skill pipeline was designed to address missing skill information.

The final recommended skills were created using:

* Existing required skills when available
* Similar job postings
* KNN-based inference
* Local LLM validation
* Rescue rules for obvious core skills
* Traceability columns to identify the skill source

### Machine Learning

The machine learning notebook includes:

* Regression models for salary prediction
* Classification models for salary bands
* Text classification for job categories
* Multi-label classification for skill prediction
* Clustering for market segmentation

---

## Project Structure

```text
2026-ai-job-market-analysis/
│
├── notebooks/
│   ├── 01_build_skill_dataset.ipynb
│   ├── 02_job_market_insights.ipynb
│   ├── 02_simplified_ai_job_market_analysis.ipynb
│   └── 03_machine_learning_analysis_ai_job_market_data.ipynb
│
├── outputs/
│   └── figures/
│       ├── coverage_by_field.png
│       ├── job_postings_by_country.png
│       ├── top_job_categories.png
│       ├── top_recommended_skills.png
│       ├── salary_distribution_us.png
│       ├── salary_by_experience_level_us.png
│       ├── job_clusters_2d.png
│       ├── rf_salary_feature_importance.png
│       ├── job_category_confusion_matrix.png
│       └── salary_band_confusion_matrix_rf.png
│
└── .gitignore
```

---

## Tools and Libraries

Main tools used:

* Python
* pandas
* numpy
* matplotlib
* seaborn
* scikit-learn
* Jupyter Notebook
* Ollama for local LLM validation
* ESCO occupations dataset for occupation mapping

---

## Important Limitations

This project is exploratory and should not be interpreted as a complete representation of the global AI job market.

Main limitations:

* Many job descriptions are truncated.
* Original required skill data is highly incomplete.
* Some final skills are inferred, not directly provided by employers.
* Salary data is incomplete.
* Salary availability varies strongly by country.
* Salaries should not be compared across countries without currency normalization.
* Job categories can overlap.
* Some job postings may be duplicated semantically even if exact duplicate rows were not present.
* Machine learning models are exploratory and not causal.

---

## Key Takeaways

The AI job market is concentrated around a few major role families, especially AI Engineer, Data Scientist, and Machine Learning Engineer.

Skill demand is broader than only model training. The dataset shows strong demand for practical skills such as Python, cloud platforms, NLP, RAG, and production-oriented AI tooling.

The original skill data was too incomplete for strong skill analysis, but the enrichment pipeline created a more usable final skill signal.

Salary analysis is useful, especially for US postings, but exact salary prediction remains difficult because salaries are noisy, incomplete, and affected by many hidden factors.

Machine learning models can identify useful patterns in the data, especially for job category classification and salary band classification, but results should be interpreted carefully.

---

## Author

Jeremy Allemand

GitHub: [JAllemand971](https://github.com/JAllemand971)
