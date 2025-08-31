Bank Loan Performance Dashboard

1)Short description and Purpose
Interactive Power BI report that tracks loan portfolio performance: total applications, funded amounts, repayments received, average interest rate, and DTI. It classifies Good vs Bad loans from loan_status, shows MTD and MoM trends, and lets users slice by state, grade, purpose, term, employment length, and home ownership to monitor risk and repayment behavior.

2)Tech Stack
Power BI Desktop
DAX (measures for KPIs, MTD/MoM, Good/Bad segmentation)
Power Query (M) for data import/typing
CSV data (financial_loan (1).csv)
Date table (Date Table) used by time-intelligence measures

3)Data Source (What the structured)
Main table: Bank_loan with columns
id, address_state, application_type, emp_length, emp_title, grade, home_ownership, issue_date, last_credit_pull_date, last_payment_date, loan_status, next_payment_date, member_id, purpose, sub_grade, term, verification_status, annual_income, dti, installment, int_rate, loan_amount, total_acc, total_payment
calculated column Good VS Bad Loan (maps loan_status → “Good Loan” for Current/Fully Paid, “BAD LOAN” for Charged Off).
Supporting table: Date Table (with Year/Month/Quarter columns) for time intelligence; Select Measure (disconnected helper for measure pickers).

4)Featured / Highlight

KPI cards: Total_loan_Applications, Total_Funded_Amount (SUM(loan_amount)), Total_Amount_Received (SUM(total_payment)), Average_interest_rate (AVERAGE(int_rate)), Average_dti (AVERAGE(dti)).
Good vs Bad Loan breakdown using Good VS Bad Loan calculated column + measures:
Good_Loan_Application / Bad_Loan_Application
Good_Loan_Funded_Amount / Bad_Loan_Funded_Amount
Good_Loan_Received_Amount / Bad_Loan_Received_Amount

Time intelligence:
MTD: TOTALMTD(...) over 'Date Table'[Date]
PMTD: DATESMTD(DATEADD('Date Table'[Date], -1, MONTH))
MoM deltas: (MTD - PMTD) / PMTD
Flexible slicing: Loan Status, State, Grade, Purpose + a “Select Measure” helper to switch focus in visuals.
Pages: Summary, Overview, Details (transaction table with totals).

5)The Best Dashboard explanation format
Business Problem
Credit/risk teams need a unified, drillable view of loan health to reduce charge-offs, target approvals, and improve collections—without waiting for ad-hoc extracts.
Goal of dashboard
Provide an at-a-glance portfolio health view with Good vs Bad segmentation, MTD/MoM performance, and demographic/behavioral breakdowns to guide policy and operational actions.

Walk through of key visuals (Briefly)
Summary: Top KPIs + Good/Bad loan cards; MTD values and MoM change indicators for quick trend checks.
Overview: Applications by Month, Term (≈36 vs 60 months split), Employee Length, Purpose (e.g., debt consolidation dominance), and Home Ownership (e.g., RENT vs MORTGAGE).
Details: Row-level table (id, purpose, grade, sub_grade, issue_date, loan_amount, int_rate, installment, total_payment) to audit and export with the same slicers.

Business impact and insights
Portfolio quality: Share of Good (Current + Fully Paid) vs Bad (Charged Off) instantly visible—supports underwriting tweaks and collection strategies.
Cash flow view: Compare Total Funded vs Total Received to watch recovery and profitability signals.
Operational levers: Identify high-risk pockets by purpose/grade/state and adjust pricing, limits, or verification rules.
Recent momentum: MTD/MoM helps spot acceleration/slowdowns early, enabling faster interventions.

6)Screenshots https://github.com/adityajangam90045/Bank_Loan-Dashboard/blob/main/Bank_dashboard.pdf


