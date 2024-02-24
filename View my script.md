# Bank-loan-details-analysis
This is analysis of bank loan details


-- Total loan application ?

 select count(application_type) from bankloan

 --2 MTD Sales
  
  SELECT COUNT(id) AS Total_Applications FROM bankloan
WHERE MONTH(issue_date) = 12

--3 PMTD Loan Applications
SELECT COUNT(id) AS Total_Applications FROM bankloan
WHERE MONTH(issue_date) = 11

--4 Total Funded Amount

SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bankloan

--5. MTD Total Funded Amount

SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bankloan
WHERE MONTH(issue_date) = 12

--6. PMTD Total Funded Amount

SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bankloan
WHERE MONTH(issue_date) = 11

--7. Total Amount Received
SELECT SUM(total_payment) AS Total_Amount_Collected FROM bankloan

--8.MTD Total Amount Received

SELECT SUM(total_payment) AS Total_Amount_Collected FROM bankloan
WHERE MONTH(issue_date) = 12

--9 . PMTD Total Amount Received

SELECT SUM(total_payment) AS Total_Amount_Collected FROM bankloan
WHERE MONTH(issue_date) = 11

--10. Average Interest Rate

SELECT AVG(int_rate)*100 AS Avg_Int_Rate FROM bankloan
 
--11. MTD Average Interest

SELECT AVG(int_rate)*100 AS MTD_Avg_Int_Rate FROM bankloan
WHERE MONTH(issue_date) = 12
 
--12. PMTD Average Interest

SELECT AVG(int_rate)*100 AS PMTD_Avg_Int_Rate FROM bankloan
WHERE MONTH(issue_date) = 11
 
--13. Avg DTI

SELECT AVG(dti)*100 AS Avg_DTI FROM bankloan
 
--14. MTD Avg DTI

SELECT AVG(dti)*100 AS MTD_Avg_DTI FROM bankloan
WHERE MONTH(issue_date) = 12
 
--15. PMTD Avg DTI

SELECT AVG(dti)*100 AS PMTD_Avg_DTI FROM bankloan
WHERE MONTH(issue_date) = 11
 
-- GOOD LOAN ISSUED
-- Good Loan Percentage

SELECT
    (COUNT(CASE WHEN loan_status = 'Fully Paid' OR loan_status = 'Current' THEN id END) * 100.0) / 
	COUNT(id) AS Good_Loan_Percentage
FROM bankloan
 
-- Good Loan Applications

SELECT COUNT(id) AS Good_Loan_Applications FROM bankloan
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current'
 
-- Good Loan Funded Amount

SELECT SUM(loan_amount) AS Good_Loan_Funded_amount FROM bankloan
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current'
 
-- Good Loan Amount Received

SELECT SUM(total_payment) AS Good_Loan_amount_received FROM bankloan
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current'
 

-- BAD LOAN ISSUED
-- Bad Loan Percentage

SELECT
    (COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100.0) / 
	COUNT(id) AS Bad_Loan_Percentage
FROM bankloan
 
-- Bad Loan Applications

SELECT COUNT(id) AS Bad_Loan_Applications FROM bankloan
WHERE loan_status = 'Charged Off'
 
-- Bad Loan Funded Amount

SELECT SUM(loan_amount) AS Bad_Loan_Funded_amount FROM bankloan
WHERE loan_status = 'Charged Off'
 
-- Bad Loan Amount Received

SELECT SUM(total_payment) AS Bad_Loan_amount_received FROM bankloan
WHERE loan_status = 'Charged Off'
 

-- LOAN STATUS DETAILS
	
 SELECT
        loan_status,
        COUNT(id) AS LoanCount,
        SUM(total_payment) AS Total_Amount_Received,
        SUM(loan_amount) AS Total_Funded_Amount,
        AVG(int_rate * 100) AS Interest_Rate,
        AVG(dti * 100) AS DTI
    FROM
        bankloan
    GROUP BY
        loan_status
 
 -- MTD

SELECT 
	loan_status, 
	SUM(total_payment) AS MTD_Total_Amount_Received, 
	SUM(loan_amount) AS MTD_Total_Funded_Amount 
FROM bankloan
WHERE MONTH(issue_date) = 12 
GROUP BY loan_status
 
-- B.	BANK LOAN REPORT | OVERVIEW
-- MONTH

SELECT 
	MONTH(issue_date) AS Month_Munber, 
	DATENAME(MONTH, issue_date) AS Month_name, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bankloan
GROUP BY MONTH(issue_date), DATENAME(MONTH, issue_date)
ORDER BY MONTH(issue_date)
 

-- STATE

SELECT 
	address_state AS State, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bankloan
GROUP BY address_state
ORDER BY address_state
 
 -- TERM

SELECT 
	term AS Term, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bankloan
GROUP BY term
ORDER BY term
 

-- EMPLOYEE LENGTH

SELECT 
	emp_length AS Employee_Length, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bankloan
GROUP BY emp_length
ORDER BY emp_length
 
-- PURPOSE

SELECT 
	purpose AS PURPOSE, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bankloan
GROUP BY purpose
ORDER BY purpose
 
-- HOME OWNERSHIP

SELECT 
	home_ownership AS Home_Ownership, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bankloan
GROUP BY home_ownership
ORDER BY home_ownership
 
-- Dataset and power bI dashboard  is added to the repository
