
# Bank-Loan-Analysis-

To effectively monitor and evaluate a bank's lending operations and overall performance, a comprehensive Bank Loan Report is essential, providing critical insights into key loan-related metrics and their trends over time, enabling the bank to enhance profitability analysis, strengthen risk assessment, inform data-driven decision making, and tailor loan products and marketing strategies to specific customer segments.

## Database and tools used :

   Database : **`SQL Server`**
   
   Reporting tool : **`Power BI`**
   
Power BI functionalities used :
Connecting to SQL Server,
Data Cleaning,
Data Modelling,
Data Processing,
Power Query,
Date Tables,
Time Intelligence Func,
DAX,
Date Function,
Text Function,
Filter Function,
Calculate,
SUM/ SUMX,
Creating KPI’s,
New Card Visual,
Creating Charts,
Formatting visuals,
Creating Functions,
Navigations.

   
Sample data is loaded in to SQL server from CSV file and dashboard is created by connecting SQL sever as source form Power BI.SQL queries were used to validate report results for thier accuracy .
  
## Report Link: 

https://app.powerbi.com/view?r=eyJrIjoiMzI4MGU1Y2QtNjJiZi00NGFmLTg3OGEtZDU4ZjA4NGZhNGIyIiwidCI6IjYyOTA2MWUyLTg4MGMtNDI4Zi1iMTIxLWY5NjYxMDVlMmFhMyJ9
## Dashboard Screenshots:
 Dashboard has 3 tabs for selection
 
 Summary tab
 
 Overview tab
 
 Details tab
 
### Summary tab :
Provides summary details on key metrics such as Total Loan Applications,Total Funded Amount,Total Amount Received,Average Interest Rate,Average Debt-to-Income Ratio, Good Loan Vs Bad loans issued for the financial year 2023.

<img width="853" alt="summary2024-11-14 132505" src="https://github.com/user-attachments/assets/8c9ff3ee-170f-439b-afd3-62103f05d4c6">

### KPI's overview :

 #### (1). Total Loan Applications:  
 This is used to calculate the total number of loan applications  received during a specified period. Additionally, it is essential to monitor the Month-to-Date (MTD) Loan Applications and track changes Month-over-Month (MoM).

 ###### Metric Calculation:
 
     Total Loan Applications = COUNT(bank_loan_data[id])

     MTD Loan Applications = CALCULATE(TOTALMTD([Total Loan Applications],'Date Table'[Date]))

     MOM Loan Application = ([MTD Loan Applications] - [PMTD Loan Applications])/[PMTD Loan Applications]
     where
     PMTD Loan Applications = CALCULATE([Total Loan Applications],DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))
####  (2). Total Funded Amount:
Understanding the total amount of funds disbursed as loans is crucial. Bank also want to keep an eye on the Month-to-Date (MTD) Total Funded Amount and analyse the Month-over-Month (MoM) changes in this metric.

 ###### Metric Calculation:
 
     Total Funded Amount = sum(bank_loan_data[loan_amount])

     MTD Funded Amount = CALCULATE(TOTALMTD([Total Funded Amount],'Date Table'[Date]))

     MOM Funded Amount = ([MTD Funded Amount] - [PMTD Total Funded Amount])/[PMTD Total Funded Amount]

     where
     PMTD Total Funded Amount = CALCULATE([Total Funded Amount],DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))
    
#### (3). Total Amount Received:
Tracking the total amount received from borrowers is essential for assessing the bank's cash flow and loan repayment. Bank wants to analyse the Month-to-Date (MTD) Total Amount Received and observe the Month-over-Month (MoM) changes.

 ###### Metric Calculation:
 
     Total Amount Received = SUM(bank_loan_data[total_payment])

     MTD Amount Recieved = CALCULATE(TOTALMTD([Total Amount Received],'Date Table'[Date]))
     
     MOM Amount Recieved = ([MTD Amount Recieved] - [PMTD Amount Recieved])/[PMTD Amount Recieved]
     
     where
     PMTD Amount Recieved = CALCULATE([Total Amount Received],DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))
#### (4). Average Interest Rate: 
Calculating the average interest rate across all loans, MTD, and monitoring the Month-over-Month (MoM) variations in interest rates will provide insights into bank lending portfolio's overall cost.

 ###### Metric Calculation:
 
     Avg Interest Rate = AVERAGE(bank_loan_data[int_rate])

     MTD Avg Interest Rate = CALCULATE(TOTALMTD([Avg Interest Rate],'Date Table'[Date])
     
     MOM Avg Interest Rate = ([MTD Avg Interest Rate] - [PMTD Avg Inerest Rate])/[PMTD Avg Inerest Rate]

     where
     PMTD Avg Inerest Rate = CALCULATE([Avg Interest Rate],DATESMTD(DATEADD('Date Table'[Date],-1,MONTH))))
 
#### (5). Average Debt-to-Income Ratio (DTI): 
Evaluating the average DTI for bank borrowers helps bank to gauge their financial health. Bank wants to compute the average DTI for all loans, MTD, and track Month-over-Month (MoM) fluctuations.

 ###### Metric Calculation:
 
     AVG DTI = AVERAGE(bank_loan_data[dti])

     MTD Avg DTI = CALCULATE(TOTALMTD([AVG DTI],'Date Table'[Date]))
     
     MOM DTI = ([MTD Avg DTI] - [PMTD Avg DTI])/[PMTD Avg DTI]

     where
     PMTD Avg DTI = CALCULATE([AVG DTI],DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))
    
### Overview tab :

I aim to visually represent critical loan-related metrics and trends using a variety of chart types. These charts will provide a clear and insightful view of bank lending operations, facilitating data-driven decision-making and enabling bank to gain valuable insights into various loan parameters

<img width="853" alt="Verview2024-11-14 132605" src="https://github.com/user-attachments/assets/a1c926dc-b4c1-481c-b825-1a8e892da2a1">

### Details tab :
'Details Dashboard' that provides a consolidated view of all the essential information within bank loan data. This Details Dashboard aims to offer a holistic snapshot of key loan-related metrics and data points, enabling users to access critical information efficiently.

<img width="851" alt="Details2024-11-14 132632" src="https://github.com/user-attachments/assets/1ec41441-5302-4ae3-b770-ee87d6f01e52">

## Graphical representation of data:

### Good Loans issued:

<img width="440" alt="Goodloanissued" src="https://github.com/user-attachments/assets/eccdffc0-8e2a-45f7-9497-28dc4d11c2a2">



Loan is considerded good when loan status is 'Fully Paid' or 'Current'. This donut chart will track following metrics :


##### Good Loan Issued Percentage

     Good Loan % = (CALCULATE(bank_loan_data[Total Loan Applications],bank_loan_data[Good Vs Bad Loan]="Good Loan"))/bank_loan_data[Total Loan Applications]
   
     where
   
     [Good Vs Bad Loan] is group created by considering field loan_status. It has 2 members .

       1. "Good Loan"
       2. "Bad Loan"

       A loan is considered "Good Loan" if loan_status is "Current" or "Fully Paid"

       A loan is considered "Bad Loan" if loan_status is "Current" or "Charged Off"
       
Group creation screenshot:

<img width="554" alt="Screenshot 2024-11-21 132428" src="https://github.com/user-attachments/assets/8bad21bd-b624-4acd-a5fa-1ef615874bee">


##### Good Loan Applications

      Good Loan Applications = CALCULATE([Total Loan Applications],bank_loan_data[Good Vs Bad Loan] = "Good Loan")

##### Good Loan Funded Amount

      Good Loan Funded Amount = CALCULATE([Total Funded Amount],bank_loan_data[Good Vs Bad Loan] = "Good Loan")

##### Good Loan Total Received Amount

      Good Loan Received Amount = CALCULATE([Total Amount Received],bank_loan_data[Good Vs Bad Loan] = "Good Loan")

### Bad Loans issued:

  <img width="446" alt="badloanissued" src="https://github.com/user-attachments/assets/bdbe2b3c-69ce-424a-bfaa-a0eac5317e5a">

  
  
Loan is considerded bad when loan status is 'Charged Off'. This donut chart will track following metrics :

##### Bad Loan Issued Percentage

      Bad Loan % = (CALCULATE(bank_loan_data[Total Loan Applications],bank_loan_data[Good Vs Bad Loan]= "Bad Loan"))/bank_loan_data[Total Loan Applications]

##### Bad Loan Applications

       Bad Loan Applications = CALCULATE([Total Loan Applications],bank_loan_data[Good Vs Bad Loan] = "Bad Loan")
       
##### Bad Loan Funded Amount

      Bad Loan Funded Amount = CALCULATE([Total Funded Amount],bank_loan_data[Good Vs Bad Loan] = "Bad Loan")
      
##### Bad Loan Total Received Amount

      Bad Loan Received Amount = CALCULATE([Total Amount Received],bank_loan_data[Good Vs Bad Loan] = "Bad Loan")

### Region Distribution:

This tree map chart helps to identify regions with significant lending activity and assess regional disparities.

<img width="765" alt="TreeMap" src="https://github.com/user-attachments/assets/795a5cfb-b330-4bc2-bd9e-d6a02cb58bfa">

### Monthly Distribution:

This line chart helps to identify seasonality and long-term trends in lending activities.

<img width="355" alt="LineChart" src="https://github.com/user-attachments/assets/865aef11-6684-42ed-b3fc-270bc5cdb1ec">

### Termwise Distribution:

This donut chart will allow the client to understand the distribution of loans across various term lengths.

<img width="338" alt="loanapplictionsbyterm" src="https://github.com/user-attachments/assets/8f519203-5204-492f-8792-4d9f36a59f8d">

### Distribution of loans purpose:

This will provide a visual breakdown of loan metrics based on the stated purposes of loans, aiding in the understanding of the primary reasons borrowers seek financing

<img width="391" alt="barchart by purpose" src="https://github.com/user-attachments/assets/630c6b36-e040-4307-aab2-3a214514dbea">

### Distribution of loans by Employment term length:

This bar chart provides insghts on how lending metrics are distributed among borrowers with different employment lengths, helping us assess the impact of employment history on loan applications.

<img width="407" alt="Barchart_by emp length" src="https://github.com/user-attachments/assets/d3cd60c0-4a9e-417a-a4e0-53ec0d4c4f9a">

### Distribution of loans by home ownership:

This tree map helps for a hierarchical view of how home ownership impacts loan applications and disbursements.


<img width="668" alt="loanpurpose_treemap" src="https://github.com/user-attachments/assets/f6248731-0045-4fd1-9172-e4cff051bdd6">

