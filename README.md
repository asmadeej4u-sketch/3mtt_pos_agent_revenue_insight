# 🇳🇬 POS Agent Revenue Insights & Analytics
> **3MTT Nigeria Capstone Project | Data Analysis & Visualization Track**  
> **Fellow Name:** Ahmad Yahaya Ahmad  
> **3MTT ID:** FE/26/542636432 
> **Location Context:** Gombe, Gombe State, Nigeria  
> **Dataset Period:** March 2026 (268 Records)

---

## 📌 Executive Overview

Point of Sale (POS) agents serve as vital financial access hubs across Nigeria, bridging the gap for cash withdrawals, deposits, and bill payments. However, thousands of small operators run their businesses with **zero net profit visibility**. Uncalculated bank charges, provider commission caps, arbitrary customer fee structures, and capital lockups from un-reconciled transaction failures mean agents rarely know their true earnings.

This Capstone Project provides a complete **End-to-End Analytics Solution** that processes raw financial logs, cleans multi-channel transaction data, constructs a profit-engineered revenue model, and delivers an **interactive dashboard** with actionable recommendations to help POS agents maximize margins and eliminate downtime losses.

---

## 📊 Key Business Performance Indicators (KPIs)

| Metric | Value | Business Significance |
| :--- | :--- | :--- |
| **Total Transaction Volume** | **₦3,234,500** | Gross value processed across 268 transactions |
| **Gross Customer Fees** | **₦42,700** | Total fees collected directly from customers |
| **Provider Commissions** | **₦11,439** | Bank/Fintech platform charges deducted |
| **Total Net Profit** | **₦31,261** | **26.3% Net Margin** on customer fees |
| **Transaction Success Rate** | **92.9%** | 249 successful vs. 19 failed/reversed txns |
| **Avg Profit / Successful Tx** | **₦125.55** | Baseline net yield per successful transaction |

---

## 💡 Core Analytical Findings

### 1. Service Profitability Breakdown
* **Cash-Out (Withdrawals) Dominance:** Accounts for **68.4% of total net income** (₦21,385 across 152 transactions). Cash availability is the primary engine of POS profitability in commercial hubs like Yaba.
* **Cash-In (Deposits):** Generated ₦6,410 (20.5% profit share) across 62 transactions.
* **Bill Payments & Airtime:** Low-margin categories producing 9.3% and 1.8% of profit share respectively.

| Transaction Type | Count | Total Volume (₦) | Customer Fees (₦) | Provider Fees (₦) | Net Profit (₦) | Profit Share |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Cash-Out** | 152 | 1,672,000 | 31,400 | 10,015 | 21,385 | **68.4%** |
| **Cash-In** | 62 | 1,322,000 | 7,600 | 1,190 | 6,410 | **20.5%** |
| **Bill Payment** | 32 | 203,000 | 3,100 | 200 | 2,900 | **9.3%** |
| **Airtime** | 22 | 37,500 | 600 | 34 | 566 | **1.8%** |
| **TOTAL** | **268** | **₦3,234,500** | **₦42,700** | **₦11,439** | **₦31,261** | **100.0%** |

### 2. Hourly Demand & Peak Float Requirements
* **Afternoon Surge (12 PM – 4 PM):** Represents **55.2% of total transaction volume** (₦1,822,500) and **58.2% of net profit**. 
* **Operational Risk:** Float exhaustion during these hours directly leads to lost revenue when cash-out customers are turned away.

### 3. Network Reliability & Failure Rates
* **Tier-1 Commercial Banks:** Access Bank and First Bank achieved a **100% transaction success rate** (0 failures).
* **Fintech & Volatile Channels:** High transaction failure rates were recorded on Moniepoint (**15.6% failed**), OPay (**14.3% failed**), and Zenith Bank (**10.5% failed**), locking up agent float during peak hours.

---

## 🚀 Strategic Recommendations

1. **Dynamic Cash Float Staging:** Hold 65% of daily cash reserves ready before 11:30 AM to capture peak afternoon withdrawal demand without turning customers away.
2. **Multi-Terminal Smart Routing:** Implement a dual-POS setup (primary fintech terminal paired with a Tier-1 bank backup like Access or FirstBank). Automatically route transactions over ₦20,000 away from volatile networks during peak hours.
3. **Fee Optimization on Low-Margin Services:** Re-evaluate Airtime and Deposit pricing; transition Airtime customers to digital self-service or bundle bill payments to increase margin per customer interaction.
4. **Automated Claims Logging:** Reconcile failed transactions daily using structured logs to track pending reversals, recovering ₦15,000+ in tied-up float within 24 hours.

---

## 📁 Repository Structure

```
.
├── pos_agent_revenue_insights.xlsx   # Interactive Excel Workbook (Dashboard, Data, Pivot Engine)
├── pos_agent_executive_summary.pdf   # Publication-Ready 1-Page Executive Summary Report
├── demo_video_script.md              # 2.5-Minute Narration Script & Screen Presentation Guide
├── README.md                         # Project Documentation & Portfolio Brief
└── data/
    └── raw_pos_transactions.csv      # Raw transaction logs
```

---

## 🛠️ Tools & Technologies Used

* **Data Cleaning & Modeling:** Microsoft Excel (Advanced Formulas: `SUMIFS`, `COUNTIFS`, `IFERROR`, Pivot Tables)
* **Visual Analytics & Dashboarding:** Excel Charts & Interactive KPI Cards
* **Documentation & Reporting:** Python (`ReportLab`, `pandas`), PDF Typesetting
* **Presentation & Demo:** Loom / OBS Studio

---

## 📽️ Demo Video & Deliverable Links

* 📊 **Interactive Workbook:** [`pos_agent_revenue_insights.xlsx`](./pos_agent_revenue_insights.xlsx)
* 📄 **1-Page Executive Summary PDF:** [`pos_agent_executive_summary.pdf`](./pos_agent_executive_summary.pdf)
* 🎬 **Video Demo (YouTube / Drive):** `[Insert Your Video Link Here]`

---

## 🎓 Acknowledgments

Developed as part of the **3 Million Technical Talent (3MTT) Fellowship** program, executed by the Federal Ministry of Communications, Innovation and Digital Economy (FMCIDE) and NITDA Nigeria. Special thanks to our track mentors and learning community managers.
