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
  - Day
    ```dax
    Day = FORMAT('Date Table'[Date], "ddd")
    ```
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
  - (col) Waittime Status
    ```dax
    Waittime Status = IF('Hospital ER_Data'[Patient Waittime]<=30, "Within Target", "Target Missed")
    ```
 - (col) Admission Hour
    ```dax
    Admission Hour = HOUR('Hospital ER_Data'[Patient Admin Date])
    ```
- (col) Waittime Interval
  ```dax
  Waittime Interval = 
  SWITCH(
      TRUE(),
      'Hospital ER_Data'[Admission Hour] < 2, "00-02",
      'Hospital ER_Data'[Admission Hour] < 4, "03-04",
      'Hospital ER_Data'[Admission Hour] < 6, "05-06",
      'Hospital ER_Data'[Admission Hour] < 8, "07-08",
      'Hospital ER_Data'[Admission Hour] < 10, "09-08",
      'Hospital ER_Data'[Admission Hour] < 12, "11-12",
      'Hospital ER_Data'[Admission Hour] < 14, "13-14",
      'Hospital ER_Data'[Admission Hour] < 16, "15-16",
      'Hospital ER_Data'[Admission Hour] < 18, "17-18",
      'Hospital ER_Data'[Admission Hour] < 20, "19-20",
      'Hospital ER_Data'[Admission Hour] < 22, "21-22",
      'Hospital ER_Data'[Admission Hour] < 24, "23-24",
      "Above 24"
  )
  ``` 
8. Dashboard layout
9. Charts & Formatting
10. Insights

------------------------------------------------------

## Key Findings


## Limitations
