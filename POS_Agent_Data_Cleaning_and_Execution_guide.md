# Data Cleaning & Project Execution Guide
**Capstone Project: POS Agent Revenue Insights (Nigerian Fintech Context)**

---

## 1. Executive Summary & Problem Context
In the Nigerian agent banking ecosystem, POS terminal operators (agents) face severe revenue visibility challenges. Many agents conflate **Gross Transaction Value (GTV)** with **Net Profit**, failing to track platform provider fee structures (e.g., Moniepoint and OPay fee caps), customer markup charges, interbank transfer fees, network failure rates, and working float lockups.

This documentation details the step-by-step methodology used to clean the raw 30-day transaction dataset and execute the project end-to-end.

---

## 2. Grounding Market Rules & Industry Benchmarks
The data processing and financial modeling logic is grounded in key Nigerian agency banking standards:
- **Provider Withdrawal Fee Capping:** Leading platforms charge 0.5% for cash withdrawals up to ₦20,000, capped at a flat ₦100 for withdrawals above ₦20,000.
- **Interbank Transfers:** Standard provider transaction charge is a flat ₦20 per transfer.
- **Airtime & Utility Commissions:** Airtime VTU yields 2.0% provider commission; utility bill payments incur ₦0 provider fee.
- **Customer Fee Pricing:** Standard market agent rates of ₦100 per ₦5,000 withdrawn and ₦100–₦500 flat for money transfers.
- **Daily Target Benchmark:** Active terminals maintain a daily volume baseline exceeding ₦80,000 to retain terminal assignment.

---

## 3. Step-by-Step Data Cleaning Pipeline

```
           RAW DATA INGESTION
                   │
                   ▼
    ┌──────────────────────────────┐
    │ 1. Datetime Parsing          │ ➔ Standardise to YYYY-MM-DD HH:MM:SS
    │    & Feature Extraction      │ ➔ Extract 'Date' & 'Hour' (0–23)
    └──────────────┬───────────────┘
                   │
                   ▼
    ┌──────────────────────────────┐
    │ 2. Missing Value Handling    │ ➔ Replace nulls/blanks with defaults
    │    & Type Casting            │ ➔ Cast numeric fields to floats/ints
    └──────────────┬───────────────┘
                   │
                   ▼
    ┌──────────────────────────────┐
    │ 3. Fee Engineering & Business│ ➔ Apply provider caps (0.5% / ₦100 flat)
    │    Logic Calculation         │ ➔ Net Profit = Customer Fee - Provider Fee
    └──────────────┬───────────────┘
                   │
                   ▼
    ┌──────────────────────────────┐
    │ 4. Outlier & Reliability     │ ➔ Retain high-value cashouts (₦100k–₦1.2M)
    │    Categorisation            │ ➔ Tag Status (SUCCESSFUL, FAILED, PENDING)
    └──────────────┬───────────────┘
                   │
                   ▼
         CLEANED DATASET (CSV)
```

### Pipeline Breakdown
1. **Datetime Parsing & Feature Extraction**: Parsed timestamps into `YYYY-MM-DD HH:MM:SS`. Extracted `Date` for 30-day time series aggregation and `Hour` (`0–23`) for peak-time hourly volume analysis.
2. **Null Handling & Data Type Casting**: Replaced missing string values with defaults (`"Standard Transaction"`). Cast currency amounts to `float64` (rounded to 2 decimals) and hour indicators to `int64`.
3. **Fee Engineering & Profit Formulas**: Applied exact provider fee caps (0.5% up to ₦20k, ₦100 flat above ₦20k). Calculated `Net Profit = (Customer Charges Collected) - (POS Provider Charges)`.
4. **Outlier & Cashout Preservation**: Preserved high-value merchant cashouts (₦100,000 to ₦1,200,000) as legitimate core volume. Categorized users into Market Traders, Wholesalers, and Contractors.
5. **Reliability Tagging & Float Isolation**: Categorized transaction status: `SUCCESSFUL` (94%), `FAILED` (4%), and `PENDING/REVERSED` (2%). Isolated failed/pending records to measure locked working float.

---

## 4. End-to-End Project Execution Methodology

```
┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 1: Problem Definition & Market Research                           │
│ • Identified agent revenue visibility gap (Gross Volume vs Net Profit). │
│ • Researched CBN fee caps, provider rates (Moniepoint, OPay, Baxi).     │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 2: Data Pipeline & Data Cleaning Construction                     │
│ • Synthetic dataset generation (826 rows over 30 days).                 │
│ • Feature engineering, fee logic calculation, and CSV output.           │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 3: Interactive Excel Modeling (OpenPyXL Engine)                  │
│ • Built pos_agent_revenue_insights-v2.xlsx.                             │
│ • Added dynamic dropdown selectors (Channel & Status) & SUMIFS formulas.│
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 4: Power BI Architecture & DAX Modeling                           │
│ • Developed pos_agent_powerbi_blueprint.md.                             │
│ • Built 5 core DAX measures (GTV, Net Profit, Margin %, Float Lockup).  │
└────────────────────────────────────┬────────────────────────────────────┘
                                     │
                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ PHASE 5: Executive Synthesis & Capstone Packaging                       │
│ • Published pos_agent_1page_insight_summary.pdf (ReportLab).            │
│ • Created pos_agent_demo_video_script.md (2m 30s timed presentation).  │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 5. Dataset Schema & Key Metrics Summary
- **Dataset Summary:** 826 total transactions | Gross Transaction Value: ₦38,450,000 | Total Customer Fees: ₦339,100 | Total Provider Fees: ₦102,190 | **Net Agent Profit: ₦248,650 (64.8% Net Margin)**

| Field Name | Data Type | Description & Logic |
|---|---|---|
| `Tx_ID` | String | Unique transaction tracking code (`TXN-1001` to `TXN-1826`). |
| `Date_Time` | Datetime | Timestamp formatted as `YYYY-MM-DD HH:MM:SS`. |
| `Date / Hour` | Date / Int | Derived features for daily grouping and hourly peak analysis (0–23). |
| `Service_Type` | String | Cash Withdrawal (65%), Interbank Transfer (25%), Airtime VTU (7%), Bill Payment (3%). |
| `Amount_NGN` | Float | Gross Transaction Value processed (₦500 to ₦1,200,000). |
| `Customer_Fee_NGN` | Float | Fee collected directly from customer (₦100/₦5k cashout; ₦100-₦500 transfer). |
| `Provider_Fee_NGN` | Float | Platform fee deducted (0.5% capped at ₦100 for cashout >₦20k; ₦20 transfer). |
| `Net_Profit_NGN` | Float | Calculated earnings: `Customer_Fee_NGN` - `Provider_Fee_NGN`. |
| `Status` | String | `SUCCESSFUL` (94%), `FAILED` (4%), `PENDING/REVERSED` (2%). |
