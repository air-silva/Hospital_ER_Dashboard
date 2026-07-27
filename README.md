# Hospital Emergency Room Dashboard

## Overview
**Business Requirements:** 

**Objective:** To enhance operational efficiency and provide actionable insights into emergency room performance. 

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

1. Clean & Transform
- Assign data type
- View column statistics
- Add column:
  - `Patient Full Name`
    ```dax
    Patient Full Name = 'Hospital ER_Data'[Patient First Name] & " " & 'Hospital ER_Data'[Patient Last Name]
    ```
  - `Patient Admin Date`
    ```dax
    Patient Admin Date = DATE(YEAR('Hospital ER_Data'[Patient Admission Date]), MONTH('Hospital ER_Data'[Patient Admission Date]), DAY('Hospital ER_Data'[Patient Admission Date]))
    ```
- Remove columns: `Patient First Name`, `Patient Last Name`
- Replace Values: 'M', 'F', 'NC' => 'Male', 'Female', 'Not Confirmed' in `Patient Gender`
- Add new table: `Data Table` (columns: Date, Month, Year)
    ```dax
    Date Table = CALENDAR(MIN('Hospital ER_Data'[Patient Admission Date]), MAX('Hospital ER_Data'[Patient Admission Date]))
    ```

2. Data Modeling
- New Relationship: Date Table - Hospital ER_Data
  - Cardonality: one to many (1:*)
  - Single cross-filter direction: single

5. Data Processing
6. DAX Calculations
- No of Patients: Distinct count of patient ID to calculate number of patients 
8. Dashboard layout
9. Charts & Formatting
10. Insights

------------------------------------------------------

## Key Findings


## Limitations
