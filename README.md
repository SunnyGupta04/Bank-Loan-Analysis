# Bank-Loan-Analysis

Agenda:  To gain a thorough understanding of our lending operations and track loan performance, I designed a grid view report segmented by 'Loan Status.' This report provides valuable insights into key metrics such as 'Total Loan Applications,' 'Total Funded Amount,' 'Total Amount Repaid,' 'Month-to-Date (MTD) Funded Amount,' 'MTD Amount Repaid,' 'Average Interest Rate,' and 'Average Debt-to-Income (DTI) Ratio.' By delivering these metrics, this report enables data-driven decision-making and helps assess the overall health of our loan portfolio.


SQL Commands:

Sql Query to Fetch the data 
KPI’S
Total Loan Application:
. Select COUNT(id ) As Total_Loan_Application from "Bank_Loan_Data "
 



MTD Loan Applications (Month To Date )
. Select COUNT(id ) As MTD_Total_Loan_Application from "Bank_Loan_Data "
Where MONTH(issue_date) = 12 And YEAR (issue_date) =2021
 

Previous month loan Application :
. Select COUNT(id ) As PMTD_Total_Loan_Application from "Bank_Loan_Data "
Where MONTH(issue_date) = 11 And YEAR (issue_date) =2021
 
 
Total Funded Amount:
. Select SUM (loan_amount) As Total_funded_Amount from "Bank_Loan_Data ";
 

Total Funded Amount MTD(Month To date ):
Select SUM (loan_amount) As MTD_Total_funded_Amount from "Bank_Loan_Data "
Where MONTH (issue_date) = 12 And YEAR (issue_date) = 2021;
 
Total Funded Amount PMTD( Previous Month To date ):
Select SUM (loan_amount) As PMTD_Total_funded_Amount from "Bank_Loan_Data "
Where MONTH (issue_date) = 11 And YEAR (issue_date) = 2021;
 

Total Amount Received:

Select SUM (total_payment) As Total_Amount_Recive From "Bank_Loan_Data "; 
  
Total Amount received month To Date :
. Select SUM (total_payment) As MTD_Total_Amount_Recive From "Bank_Loan_Data "
Where MONTH(issue_date) = 12 And year (issue_date) = 2021; 
 

Total Amount received Previous month To Date:
Select SUM (total_payment) As PMTD_Total_Amount_Recive From "Bank_Loan_Data "
Where MONTH(issue_date) = 11 And year (issue_date) = 2021;
 

Average interest rate :
Select Round( AVG (int_Rate),4) *100 As Avg_intrest_rate  From "Bank_Loan_Data";
 
 
Average interest rate Month to date:
Select Round( AVG (int_Rate),4) *100 As MTD_Avg_intrest_rate  From "Bank_Loan_Data"
Where MONTH (issue_date) =12 And Year (issue_date) = 2021;
 
Average interest rate Previous Month to date:
.Select Round( AVG (int_Rate),4) *100 As PMTD_Avg_intrest_rate  From "Bank_Loan_Data"
Where MONTH (issue_date) =11 And Year (issue_date) = 2021;
 
Average DTI :
. Select Round (AVG (dti) ,4 ) *100 As Average_MTD_DTI from "Bank_Loan_Data";
 
Average DTI _Month To date (MTD) :
. Select Round (AVG (dti) ,4 ) *100 As Average_MTD_DTI from "Bank_Loan_Data"
Where MONTH (issue_date) =12  And YEAR (issue_date) =2021;
 
Average DTI _previous_Month To date (PMTD) :
Select Round (AVG (dti) ,4 ) *100 As Average_PMTD_DTI from "Bank_Loan_Data"
Where MONTH (issue_date) =11  And YEAR (issue_date) =2021;
 
Good_Loan_Precentage:

. Select (COUNT (CASE WHEN loan_status = 'Fully Paid' OR loan_status = 'Current' THEN id END)*100)
/COUNT(id) As Good_loan_Percentage 
From "Bank_Loan_Data "
 
Good Loan Application :
. Select COUNT (id) AS Good_Loan_Application from Bank_Loan_Data  
WHERE loan_status = 'Fully Paid' OR  loan_status = 'Current';
 

Good Loan Funded Amount:
. Select Sum (loan_amount) AS Good_Loan_Funded_Amount from Bank_Loan_Data  
WHERE loan_status = 'Fully Paid' OR  loan_status = 'Current';
 

Good Loan Total Received Amount :
. Select Sum (total_payment) AS Good_Loan_Total_Payment_Recived from Bank_Loan_Data  
WHERE loan_status = 'Fully Paid' OR  loan_status = 'Current';
 
Bad Loan Percentage:
. Select (COUNT (CASE WHEN loan_status = 'Charged off'  THEN id END)*100)
/COUNT(id) As Bad_loan_Percentage 
From "Bank_Loan_Data "
 

Bad Loan Application:
. Select COUNT ((id) )As Bad_Loan_Application from "Bank_Loan_Data"
WHERE loan_status ='charged off'
 
Bad Loan Funded Amount: 
. Select Sum ((loan_amount) )As Bad_Loan_Funded_Amount from "Bank_Loan_Data"
WHERE loan_status ='charged off'
 

Total Amount Received from Bad Loan:
. Select Sum ((total_payment) )As Bad_Loan_Recived_Amount from "Bank_Loan_Data"
WHERE loan_status ='charged off'
 

Loan Status:
SELECT
        loan_status,
        COUNT(id) AS LoanCount,
        SUM(total_payment) AS Total_Amount_Received,
        SUM(loan_amount) AS Total_Funded_Amount,
        AVG(int_rate * 100) AS Interest_Rate,
        AVG(dti * 100) AS DTI
    FROM
        bank_loan_data
    GROUP BY
        loan_status
 
Sum of payment Received on current Month  (December)
SELECT 
	loan_status, 
	SUM(total_payment) AS MTD_Total_Amount_Received, 
	SUM(loan_amount) AS MTD_Total_Funded_Amount 
FROM bank_loan_data
WHERE MONTH(issue_date) = 12 
GROUP BY loan_status
 

Bank loan report on monthly basis:
. SELECT 
	MONTH(issue_date) AS Month_Name, 
	DATENAME(MONTH, issue_date) AS Month_name, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY MONTH(issue_date), DATENAME(MONTH, issue_date)
ORDER BY MONTH(issue_date)


 

Bank Loan Report on address basis 
. SELECT 
	address_state AS State, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY address_state
ORDER BY address_state

 



Bank Loan Report on Term basis 
. SELECT 
	term AS Term, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY term
ORDER BY term
 

Employee Length :
SELECT 
	emp_length AS Employee_Length, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY emp_length
ORDER BY emp_length
 

Purpose:
SELECT 
	purpose AS PURPOSE, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY purpose
ORDER BY COUNT(id) DESC
 

Home Ownership:
SELECT 
	home_ownership AS Home_Ownership, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY home_ownership
ORDER BY COUNT (id) DESC
 

Technical insight:  The main goal of the Details Dashboard is to offer an intuitive and comprehensive interface for accessing essential loan data. It acts as a centralized platform for users to obtain in-depth insights into our loan portfolio, borrower profiles, and loan performance.



