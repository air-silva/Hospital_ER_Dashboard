# Hospital Emergency Room Dashboard

## Overview
**Business Requirements:** Develop a Dashboard that enables operational monitoring, demographic analysis, performance tracking, and patient‑level review. 

**Objective:** Provide insights into emergency room performance to enhance operational efficiency through a multi-view dashboard. Dashboard will contain the following:
- monitor key metrics and trends on a month-by-month basis to identify patterns and areas for improvement
- summary of hospital performance for a customisable date range
- patient-level data to enable detailed analysis and troubleshooting

### Tools
- Power BI
- DAX

---------------------------------------------

## Dataset
The [dataset]() contains patient information collected from a hospital emergency room. 

| Patient Id | Patient Admission Date | Patient First Initial | Patient Last Name | Patient Gender | Patient Age | Patient Race | Department Referral | Patient Admission Flag | Patient Satisfaction Score | Patient Waittime | Patients CM |
| ---------- | ---------------------- | --------------------- | ----------------- | -------------- | ----------- | ------------ | ------------------- | ------------------------- | -------------------------- | ---------------- | ----------- | 
| 145-39-5406	| 20/03/2024 08:47 |	H	| Glasspool	| M	| 69	| White	| None	| FALSE	| 10	| 39	| 0 |


Click [here]() to download from source.

-----------------------------------------

## Project Workflow

### 1. Clean & Transform
- Convert data types
- View column statistics
- Add and remove columns
- Replace Values
- Add new table (`Date Table`)

Open [MetaData](MetaData.md) file to view model, tables, columns, measures and their DAX expressions. 

### 2. Data Modelling
- Relationship: `Date Table` - `Hospital ER_Data`
  - Cardinality: one to many (1:*)
  - Cross-filter direction: single

### 3. Dashboard layout
- Monthly View
- Consolidated View
- Patient Details

### 4. Charts & Formatting 
- Cards
- Bar + column charts
- Line charts
- Donut Charts
- Matrix table
- Filters

### 10. Insights
See: Key Findings
- Patient wait time & Satisfaction
- Admission and departmental referrals
- Peak busy periods
- Patient demographics
- Race distribution

------------------------------------------------------

## Key Findings
The emergency room dataset covers a period of 19 months (April 2023-October 2024) and records a total of 9,216 unique patients. 

#### Patient Wait Time & Satisfaction 
- Average wait time: approx. 35.3 min. Target is 30 min. 
- Average satisfaction score: 4.99 out of 10.
  - The average satisfaction score is notably low despite a moderate average wait time. This suggests other factors beyond wait time may contribute, e.g. communication during waiting, efficiency of triage process, perceived fairness in queue progression, staff behaviour, etc.

#### Admission and Departmental Referrals
- Nearly half of the patients (4612) were admitted, while the rest (4604) were treated and released.
- A significant number of patients (5400) did not require referrals.
- Out of the referred patients, the most common were General Practice (1840) and Orthopedics (995 Cases), followed by Physiotherapy (276 Cases) and Cardiology (248 Cases).
  - High referrals to GP may indicate triage redirecting non-emergency cases and ER misuse for primary care needs. 

#### Peak busy periods
- Busiest days: Saturday (1377 Patients), Thursday (1332 Patients), and Sunday (1318 Patients).
- Busiest hours: 11-12 PM, 07-08 AM, 00-02 AM
  - Busy late night / early morning period may suggest peak is driven by evening activities or alcohol-related cases. Saturday being the busiest day may also be due to weekend social activity or reduced access to GP services.
  - This supports dynamic staffing models rather than fixed schedules. 

#### Patient demographics
- Adults (30 - 39 Years) formed a large group (1200 patients), followed by young adults (20 - 29 Years) with 1188, and children/teenagers (10 - 19 Years) with 1179 patients.
- Young children (0-9) formed the smallest group with 1056 patients.
- No significant differences between male (51.05%) and female (48.69%) patients.

#### Race distribution
- The largest racial group was White (2571), followed by African American (1951), multi racial (1557), and Asian (1060) patients.
  - Without population-level data, it's unclear whether this reflects true utilisation patterns or over/under-representation.
- A significant number of patients (1030) declined to identify their race.
  - A large 'decline to identify' group may suggest discomfort with demographic questions or inconsistent data collection practices.
