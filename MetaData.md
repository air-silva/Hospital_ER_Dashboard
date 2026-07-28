# Relationships

| From Table | From Column | To Table | To Column | Type |
| ---------- | ----------- | -------- | --------- | ---- |
| Hospital ER_Data | Patient Admin Date | Date Table | Date | Many-to-One |

# Date Table

| Column | Data Type | DAX Expression |
| --- | --- | --- |
| **Date** | Date | *(Calculated table column)* |
| **Month** | Text | ``FORMAT('Date ``Table'[Date], ``"mmm")`` |
| **Year** | Integer | ``YEAR('Date ``Table'[Date])`` |
| **Month & Year** | Text | ``'Date ``Table'[Month] ``& ``" ``" ``& ``'Date ``Table'[Year]`` |
| **Month Number** | Integer | ``MONTH('Date ``Table'[Date])`` |
| **Day** | Text | ``FORMAT('Date ``Table'[Date], ``"ddd")`` |
| **Week Day** | Integer | ``WEEKDAY('Date ``Table'[Date], ``2)`` |

# Calculated Columns
Hospital ER_Data

| Column | Data Type | DAX Expression |
| --- | --- | --- |
| **Patient Admin Date** | Date | ``DATE(YEAR('Hospital ``ER_Data'[Patient ``Admission ``Date]), ``MONTH('Hospital ``ER_Data'[Patient ``Admission ``Date]), ``DAY('Hospital ``ER_Data'[Patient ``Admission ``Date]))`` |
| **Admission Status** | Text | ``IF('Hospital ``ER_Data'[Patient ``Admission ``Flag] ``= ``TRUE, ``"Admitted", ``"Not ``Admitted")`` |
| **Age Group** | Text | ``SWITCH( ``TRUE(), ``'Hospital ``ER_Data'[Patient ``Age] ``>= ``100, ``"100+", ``'Hospital ``ER_Data'[Patient ``Age] ``>= ``90, ``"90-99", ``'Hospital ``ER_Data'[Patient ``Age] ``>= ``80, ``"80-89", ``'Hospital ``ER_Data'[Patient ``Age] ``>= ``70, ``"70-79", ``'Hospital ``ER_Data'[Patient ``Age] ``>= ``60, ``"60-69", ``'Hospital ``ER_Data'[Patient ``Age] ``>= ``50, ``"50-59", ``'Hospital ``ER_Data'[Patient ``Age] ``>= ``40, ``"40-49", ``'Hospital ``ER_Data'[Patient ``Age] ``>= ``30, ``"30-39", ``'Hospital ``ER_Data'[Patient ``Age] ``>= ``20, ``"20-29", ``'Hospital ``ER_Data'[Patient ``Age] ``>= ``10, ``"10-19", ``"0-9" ``)`` |
| **Waittime Status** | Text | ``IF('Hospital ``ER_Data'[Patient ``Waittime]<=30, ``"Within ``Target", ``"Target ``Missed")`` |
| **Admission Hour** | Integer | ``HOUR('Hospital ``ER_Data'[Patient ``Admission ``Date])`` |
| **Waittime Interval** | Text | ``SWITCH( ``TRUE(), ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``2, ``"00-02", ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``4, ``"03-04", ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``6, ``"05-06", ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``8, ``"07-08", ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``10, ``"09-10", ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``12, ``"11-12", ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``14, ``"13-14", ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``16, ``"15-16", ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``18, ``"17-18", ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``20, ``"19-20", ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``22, ``"21-22", ``'Hospital ``ER_Data'[Admission ``Hour] ``< ``24, ``"23-24", ``"Above ``24" ``)`` |

# Measures

| Name | Table | Data Type | DAX Expression |
| ---- | ----- | --------- | -------------- |
| **No of Patients** | Hospital ER_Data | Integer | ``DISTINCTCOUNT('Hospital ``ER_Data'[Patient ``Id])`` |
| **Avg Wait Time** | Hospital ER_Data | Decimal | ``FORMAT(AVERAGE('Hospital ``ER_Data'[Patient ``Waittime]), ``"0.0") ``& ``" ``" ``& ``"min"`` |
| **Satisfaction Score** | Hospital ER_Data | Decimal | ``AVERAGE('Hospital ``ER_Data'[Patient ``Satisfaction ``Score])`` |
| **No of Patients Referred** | Hospital ER_Data | Integer | ``CALCULATE(COUNTROWS('Hospital ``ER_Data'), ``'Hospital ``ER_Data'[Department ``Referral] ``<> ``"None")`` |

