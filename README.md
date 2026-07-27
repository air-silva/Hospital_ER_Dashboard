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
- Add columns:
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
  - Add columns:
  - Month
    ```dax
    Month = FORMAT('Date Table'[Date], "mmm") 
    ```
  - Year
    ```dax
    Year = YEAR('Date Table'[Date])
    ```
  - Month Number (for month sorting)
    ```dax
    Month Number = MONTH('Date Table'[Date])
    ```
  - Month & Year (for filter visual)
    ```dax
    Month & Year = 'Date Table'[Month] & " " & 'Date Table'[Year] 
    ```
2. Data Modeling
- New Relationship: Date Table - Hospital ER_Data
  - Cardonality: one to many (1:*)
  - Single cross-filter direction: single

5. Data Processing
6. DAX Calculations
- No of Patients: Distinct count of patient ID to calculate number of patients
- Avg Wait Time
  ```dax
  Avg Wait Time = FORMAT(AVERAGE('Hospital ER_Data'[Patient Waittime]), "0.0") & " " & "min"
  ```
- Satisfaction Score
  ```dax
  Satisfaction Score = AVERAGE('Hospital ER_Data'[Patient Satisfaction Score])
  ```
- No of Patients Referred
  ```dax
  No of Patients Referred = CALCULATE(COUNTROWS('Hospital ER_Data'), 'Hospital ER_Data'[Department Referral] <> "None")
  ```
- (Calc column) Admission Status
  ```dax
  Admission Status = IF('Hospital ER_Data'[Patient Admission Flag] = TRUE, "Admitted", "Not Admitted")
  ```
- (calc column) Age Group
  ```dax
  Age Group = 
  SWITCH(
      TRUE(), 
      'Hospital ER_Data'[Patient Age] >= 100, "100+",
      'Hospital ER_Data'[Patient Age] >= 90, "90-99",
      'Hospital ER_Data'[Patient Age] >= 80, "80-89",
      'Hospital ER_Data'[Patient Age] >= 70, "70-79",
      'Hospital ER_Data'[Patient Age] >= 60, "60-69",
      'Hospital ER_Data'[Patient Age] >= 50, "50-59",
      'Hospital ER_Data'[Patient Age] >= 40, "40-49",
      'Hospital ER_Data'[Patient Age] >= 30, "30-39",
      'Hospital ER_Data'[Patient Age] >= 20, "20-29",
      'Hospital ER_Data'[Patient Age] >= 10, "10-19",
      "0-9"
    )
  ```
8. Dashboard layout
9. Charts & Formatting
10. Insights

------------------------------------------------------

## Key Findings


## Limitations
