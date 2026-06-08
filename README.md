# 🏃‍♀️ Fitness Data Analysis with Alteryx

> **Case Study: Analyzing Fitness Tracker Data to uncover user behavior, activity patterns, and health insights using Alteryx Designer**

![Alteryx](https://img.shields.io/badge/Alteryx-0078C1?style=for-the-badge&logo=alteryx&logoColor=white)
![DataCamp](https://img.shields.io/badge/DataCamp-Certified-03EF62?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Business Questions](#-business-questions)
- [Dataset](#-dataset)
- [Analysis Workflow](#-analysis-workflow)
- [Key Findings](#-key-findings)
- [Repository Structure](#-repository-structure)
- [Tools Used](#️-tools-used)
- [Certification](#-certification)
- [About Me](#-about-me)

---

## 📖 Project Overview

This project is a **DataCamp Case Study** completed as part of the *Analyzing Fitness Data in Alteryx* course. The scenario is based on **Bellabeat**, a company that designs smart fitness-tracking products for women, seeking to grow its customer base by understanding user habits.

The analysis follows a structured 5-step data flow:

```
Business Question → Data Check → Data Cleaning → Data Analysis → Consolidate & Share
```

The goal was to use Alteryx to prepare, transform, and analyze fitness tracker data from 30 users over 31 days, then answer key business questions to support marketing and product strategy.

---

## ❓ Business Questions

1. What is the **predominant lifestyle** based on the lifestyle index?
2. How do users' **physical activity levels** compare to WHO/CDC recommended norms?
3. Are there any **patterns in activity/exercise schedules** by weekday?
4. What are the **most tracked activities** among users?

---

## 📊 Dataset

The dataset is sourced from Kaggle (FitBit Fitness Tracker Data) and contains personal fitness tracker data from **30 users over 31 days** across three CSV files:

| File | Description | Key Columns |
|------|-------------|-------------|
| `DailyActivity.csv` | Daily physical activity metrics | Id, ActivityDate, TotalSteps, Calories, VeryActiveMinutes, SedentaryMinutes... |
| `SleepDay.csv` | Daily sleep records | Id, SleepDay, TotalMinutesAsleep, TotalTimeInBed |
| `WeightLogInfo.csv` | Daily weight logs | Id, Date, WeightKg, HeightMeters, Fat |

**Data Quality Notes:**
- All fields initially loaded as `V_String` type — required data type conversion
- 65 NULL values found in the `Fat` column of WeightLogInfo
- SleepDay had 3 duplicate rows
- Unique IDs: DailyActivity (24), WeightLogInfo (8), SleepDay (33)
- Average step count exceeded 8,000 on only 11 out of 31 days

---

## 🔄 Analysis Workflow

The project is organized into **3 chapters**, each building on the previous:

### Chapter 1 — Data Import, Cleaning & Exploration
| Workflow File | What It Does |
|---|---|
| `1_1_importing_data_and_modifying_data_type.yxmd` | Imports all 3 CSVs; converts V_String fields to correct data types (numeric, date) |
| `1_2_finding_and_replacing_null_values.yxmd` | Scans data profiles for NULLs; replaces NULL Fat values with 0 |
| `1_3_count_unique_ids_and_find_duplicate_rows.yxmd` | Counts unique user IDs per dataset; identifies and removes 3 duplicate rows in SleepDay |
| `1_4_find_average_steps.yxmd` | Calculates average daily steps across all users; filters days where avg steps > 8,000 |

### Chapter 2 — Feature Engineering & Health Metrics
| Workflow File | What It Does |
|---|---|
| `2_1_date_conversion_dataset_integration.yxmd` | Converts string dates to proper date format; joins all 3 datasets on Id + Date |
| `2_2_calculate_BMI.yxmd` | Computes BMI using `WeightKg / HeightMeters²`; identifies users with Normal BMI (< 24.9) |
| `2_3_find_lifestyle_index.yxmd` | Classifies each user's average daily steps into lifestyle categories: Sedentary, Low Active, Somewhat Active, Active, Very Active |
| `2_4_find_sitting_threshold.yxmd` | Calculates sedentary minutes and awake sedentary hours; categorizes users by sitting health risk level (Low / Medium / High / Very High) |

### Chapter 3 — Behavioral Patterns & WHO Compliance
| Workflow File | What It Does |
|---|---|
| `3_1_find_sedentary_minutes%.yxmd` | Calculates % of total waking time spent sedentary per user |
| `3_2_find_sleep_pattern.yxmd` | Aggregates average minutes asleep vs. time in bed by weekday; identifies sleep quality patterns |
| `3_3_find_step_count_pattern.yxmd` | Computes average step count by day of week; shows which days users are most/least active |
| `3_4_weekly_activity_analysis.yxmd` | **Complete end-to-end solution**: calculates weekly MVPA (Moderate-to-Vigorous Physical Activity) minutes; compares against the WHO guideline of 150 min/week; categorizes users as Above or Below threshold |

---

## 🔍 Key Findings

| Category | Finding |
|---|---|
| **Lifestyle** | Majority of users fall into "Somewhat Active" (10 users) and "Low Active" (9 users) categories |
| **BMI** | Only 3 users out of 8 with weight data had a Normal BMI (< 24.9) |
| **Sitting Risk** | 8 users at Very High or High sitting risk; 16 users at Medium or Low risk |
| **WHO Compliance** | Most users fail to hit the 150 min/week MVPA threshold in most weeks |
| **Step Count** | Average daily steps exceeded the 8,000-step benchmark on only 11 days |
| **Sleep Patterns** | Sleep quality (minutes asleep vs. time in bed) varies meaningfully by day of week |

---

## 📂 Repository Structure

```
alteryx-fitness-data-analysis/
│
├── datasets/                          # Source CSV files used in the analysis
│   ├── DailyActivity.csv
│   ├── SleepDay.csv
│   └── WeightLogInfo.csv
│
├── workflows/                         # All Alteryx workflow (.yxmd) files
│   ├── chapter1/
│   │   ├── 1_1_importing_data_and_modifying_data_type.yxmd
│   │   ├── 1_2_finding_and_replacing_null_values.yxmd
│   │   ├── 1_3_count_unique_ids_and_find_duplicate_rows.yxmd
│   │   └── 1_4_find_average_steps.yxmd
│   ├── chapter2/
│   │   ├── 2_1_date_conversion_dataset_integration.yxmd
│   │   ├── 2_2_calculate_BMI.yxmd
│   │   ├── 2_3_find_lifestyle_index.yxmd
│   │   └── 2_4_find_sitting_threshold.yxmd
│   └── chapter3/
│       ├── 3_1_find_sedentary_minutes%.yxmd
│       ├── 3_2_find_sleep_pattern.yxmd
│       ├── 3_3_find_step_count_pattern.yxmd
│       └── 3_4_weekly_activity_analysis.yxmd   ← Complete end-to-end solution
│
├── docs/
│   └── certification.pdf              # DataCamp completion certificate
│
├── README.md
└── LICENSE
```

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **Alteryx Designer** | Data preparation, transformation, and analysis |
| **Alteryx Tools Used** | Input Data, Data Profiling, Select, Filter, Summarize, Formula, Join, Unique, Sort, Multi-Row Formula |
| **CDC / NIH Guidelines** | Benchmark for BMI and sitting thresholds |
| **WHO Guidelines** | Benchmark for weekly physical activity (150 min MVPA) |

---

## 🏅 Certification

This case study was completed as part of the **DataCamp** course:
> *Case Study: Analyzing Fitness Data in Alteryx* — Completed June 07, 2026 (3 hours)

Certificate available in `/docs/certification.pdf`

---

## 🌟 About Me

Hi, I'm **Disha Jain** — an IT professional building expertise in data analytics and engineering.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/dishadineshjain)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/dishajain-dataanalyst)

**Other Projects:**
- [SQL Data Warehouse Project](https://github.com/dishajain-dataanalyst/sql-data-warehouse-project)
- [SQL Data Analytics Project](https://github.com/dishajain-dataanalyst/sql-data-analytics-project)
- [Power BI AdventureWorks](https://github.com/dishajain-dataanalyst/powerbi-adventureworks)
