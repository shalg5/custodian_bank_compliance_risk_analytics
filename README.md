# 💼 BNY Custodian Bank Risk Analytics  
### *A Data-Driven Approach to Detect AML, KYC, and Liquidity Risks in Custodian Banking*

---

## 📘 Project Overview

This project replicates a **custodian bank risk management framework**, inspired by real-world bank operations.  
It uses a multi-table dataset — *Customers, Accounts, Transactions, Loans, and Addresses* — to build an integrated analytics model for compliance and liquidity monitoring.

The goal was to identify and quantify hidden risks through data-driven insights across three domains:

1. **Anti-Money Laundering (AML) Detection**
2. **KYC Data Integrity & Relationship Validation**
3. **Cash Flow & Liquidity Risk Monitoring**

All analysis was performed in **Excel and Power Query**, emphasizing logic reproducibility and audit transparency.

---

## 🎯 Business Problems

**1️⃣ Laundering Risk Identification**  
How can we detect hidden structuring activity when no transaction exceeds the $10,000 reporting threshold?

**2️⃣ KYC Data Relationship & Consistency**  
Which customers have missing or inconsistent identity data that could expose compliance weaknesses?

**3️⃣ Cash Flow & Liquidity Health**  
Which customers or segments show negative net cash positions or high outflow ratios indicating settlement stress?

---

## 🧠 Analytical Logic & Methodology

### AML – Laundering Risk Detection

**Objective:** Detect repetitive small-value transactions below the CTR threshold to flag potential structuring behavior.

**Steps:**
- Grouped transactions by CustomerID and week.  
- Counted total transactions and total transaction value.  
- Applied AML rule to flag potential laundering:
```m
if [TransactionCount] >= 3 and [TotalAmount] >= 1000 and [TotalAmount] <= 10000 
   then "Laundering Risk" 
   else "Normal"
   ```
- Segmented results by account type (Checking, Business, Payroll, etc.).

**Visualization:**
- 📊 Bar chart of risky customers by week.  
- 🎯 KPI: % of customers flagged under laundering risk.

**Business Insight:**  
Even without large transactions, repeated sub-$10K activities revealed **structured transaction behavior**.  
BNY-style custodians can use this model to monitor **micro-structuring** patterns in domestic activity.

---

### 👤 KYC – Data Completeness & Relationship Validation

**Objective:**  
Assess the completeness and quality of customer identity data for regulatory readiness.

**Approach:**
- Checked for missing **name** fields.  
- Checked for missing **address** fields.  
- Checked for missing **account linkage**.  
- Calculated a composite **KYC Score** based on data completeness: ```m (if [Missing Name Details]="Y" then 3 else 0) + (if [Missing Address]="Y" then 3 else 0) + (if [No Account Flag]="Y" then 4 else 0)```
- Segmented KYC risk levels (Low / Medium / High) based on score ranges.

**Visualization:**
- 📊 Bar chart: Missing KYC fields by CustomerType.  
- 📈 KPI: Average KYC Score across customer segments.  
- 🚨 Highlight: Customers with KYC Score ≥ 6 flagged for review.

**Business Insight:**  
The analysis exposed **incomplete customer records** that weaken compliance and audit readiness.  
It helps custodians prioritize data remediation and strengthen **Customer Identification Program (CIP)** adherence.

---

### 💧 Liquidity – Cash Flow & Outflow Ratio Analysis

**Objective:**  
Evaluate customer-level cash flow and liquidity pressure based on inflows and outflows.

**Approach:**
- Classified transactions into **Inflow** (Deposits, Transfers) and **Outflow** (Withdrawals, Payments).  
- Aggregated totals by CustomerID to compute:
- **TotalInflow**  
- **TotalOutflow**  
- **NetPosition = TotalInflow – TotalOutflow**  
- **OutFlowRatio = TotalOutflow / (TotalInflow + TotalOutflow)**
- Defined liquidity risk levels:
- High Risk: OutFlowRatio > 0.7 or negative NetPosition  
- Medium Risk: OutFlowRatio between 0.5–0.7  
- Low Risk: OutFlowRatio ≤ 0.5

**Visualization:**
- 📊 Bar Chart: OutFlowRatio by CustomerType.  
- 📈 KPI: % of high-risk customers by segment.  
- 📉 Chart: Inflow vs Outflow trends per customer.

**Business Insight:**  
Approximately **15% of customers** showed high OutFlowRatio values, signaling potential funding strain.  
Tracking liquidity behavior helps custodians manage **settlement risk** and maintain cash flow stability.

---

## 🔍 Key Insights

- Repetitive sub-$10K transfers highlighted **potential structuring risks**.  
- Incomplete KYC records revealed **data quality and audit readiness gaps**.  
- OutFlowRatio analysis exposed **liquidity concentration risk** among a small subset of customers.  
- Combining these dimensions provided a holistic **risk visibility framework** for custodial banking operations.

---

## ⚠️ Business Risks

**AML**  
- Increased fund movement through frequent payments between business or payroll accounts.  
- The current AML focus on transactions alone overlooks risk links across deposits, payments, and loans.

**KYC**  
- Multiple customers linked to one address suggest related-party or nominee structures.  
- Mismatched or missing linkages between loan and account data imply false identity or product misuse.

**Cash Flow & Liquidity**  
- A small group of clients drives most outflows, increasing dependency and liquidity stress risk.  
- Internal transfers between a client’s own accounts overstate inflow strength, masking funding gaps.

---

## 💡 Business Recommendations

**AML**  
- Continuously monitor B2B transactions, payments, and transfers.  
- Combine AML insights from deposits, loans, and payments to track total fund movement.

**KYC**  
- Group customers by address to detect clusters for enhanced due diligence.  
- Enforce KYC consistency across accounts, loans, and customer records.

**Cash Flow & Liquidity**  
- Track top outflow contributors and set segment-specific exposure limits.  
- Exclude self-transfers to calculate true external liquidity and support Treasury stress testing.

---

## 🧠 Challenges & Limitations

- Dataset covered a **short time frame** and limited transaction volume.  
- No **cross-border or multi-currency data**, restricting AML scenario testing.  
- Missing **timestamps** prevented intra-day cash flow monitoring.  
- No **industry or customer segment details**, limiting behavioral segmentation.  
- Dataset lacked connectivity between **loan repayment and collateral information**, reducing liquidity depth.

---

## 🏁 Conclusion

This project demonstrates how **data analytics strengthens compliance and liquidity oversight** in a custodian bank.  
By uniting AML, KYC, and liquidity perspectives, the analysis establishes a foundation for **proactive risk monitoring** and smarter, data-driven decision-making.


