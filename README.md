# Health-care-project-Power_BI
The healthcare dataset includes patient info across multiple departments and services. It tracks metrics like appointment attendance, treatment success rates, costs, and resource utilization. It also covers patient demographics, satisfaction, health outcomes, and factors influencing service efficiency and patient care quality.

## Questions :
  - Billing Amount
  - Medication Cost
  - Treatment Cost
  - Total Insurance
  - Room Charges
  - Out of Pocket
  - calculate the average for each of the KPI's
  - Analyze the total Billing Amount By State and city
  - Total Billing Amount by Procedure with the percentage of Grand Total
  - Total Billing Amount by Diagnosis and service type
  - Total Billing Amount by Department with Pct of Grand Total

## Process_Steps :
1. Cleaning data in power Query 
2. Data Modelling 
3. Calculate Using Dax
4. Visualize data

![Health care project](https://github.com/user-attachments/assets/a1520757-990c-457b-9cb8-a2e948ef8af5)


https://github.com/user-attachments/assets/b1c97d53-23ee-4318-a412-fe1ee5f241bb


## Some calculation by DAX

- date = 

ADDCOLUMNS(
    CALENDARAUTO(5),
    "Year", YEAR([Date]),
    "date of months", DAY([Date]),
    "Months",FORMAT([Date],"mmm"),
    "Months Number", MONTH([Date]),
    "Day", FORMAT([Date],"ddd"),
    "day number" , WEEKDAY([Date]),
    "Quatar", "Q-"& FORMAT([Date],"q"),
    "Day type", IF(WEEKDAY([Date])=1 || WEEKDAY([Date])=7, "Weekend","Week day")
)

- lenth of stay = IF(DATEDIFF(visits[Admitted Date],visits[Discharge Date],DAY) > 0,DATEDIFF(visits[Admitted Date],visits[Discharge Date],DAY),0)

- % deperment = DIVIDE([total billing amount],
                        CALCULATE([total billing amount],ALL(departments[Department])))

- active colume name = SELECTEDVALUE(departments[Department])

- blank = 0

- total bill by % = 
    DIVIDE([total billing amount],
        CALCULATE([total billing amount],ALL(procedures[Procedure])))

- total Bill from pocket = [total billing amount] - [total Insurance Coverage]

- total billing amount = ([total rent of room]+[total Medical cost]+[total Treatment Cost])- [total Insurance Coverage]

- total Insurance Coverage = SUM(visits[Insurance Coverage])

- total Medical cost = SUM(visits[Medication Cost] )

- total patients = DISTINCTCOUNT(patients[Patient ID])

- total rent of room = SUMX(visits,visits[lenth of stay] * visits[Room Charges(daily rate)])

- total Treatment Cost = SUM(visits[Treatment Cost])

- Avg Bill from Pocket = [total Bill from pocket]/[total patients]

- Avg Billing = DIVIDE([total billing amount],[total patients])

- Avg Insurance = AVERAGE(visits[Insurance Coverage])

- Avg Medical cost = AVERAGE(visits[Medication Cost])

- Avg Rent of room = DIVIDE([total rent of room],[total patients])

- Avg Treatment = AVERAGE(visits[Treatment Cost])



