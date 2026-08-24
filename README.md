# ☕ Cafe Rewards Analytics Dashboard

An end-to-end **Power BI analytics project** designed to evaluate customer behavior, promotional offer engagement, transaction performance, offer effectiveness, communication channels, and customer segments for a cafe rewards program.

The project uses **Power Query for data cleaning and transformation**, **data integration for preparing the analytical model**, and **DAX for creating business KPIs and measures**.

---

## 📌 Project Overview

The objective of this project is to understand how effectively the cafe's rewards program is performing.

The analysis focuses on:

- Customer demographics and segmentation
- Offer engagement and customer response
- Offer-associated vs. non-offer transactions
- Offer type performance
- Communication channel effectiveness
- Transaction and spending behavior
- Customer segments contributing to offer-associated spending

The final output is an interactive **Power BI dashboard** containing an Overview page and a Key Drivers page.

---

# 🎯 Business Problem

The cafe wants to understand how effectively its customer rewards program is performing.

Management needs to know:

- How customers engage with promotional offers
- Which offers perform better
- Which communication channels generate stronger transaction rates
- How offer-associated transactions compare with non-offer transactions
- Which customer segments contribute the most spending
- Where customers drop off during the offer journey

The raw data required cleaning, transformation, and integration before meaningful analysis could be performed.

---

# ❓ Business Questions

### Customer Analysis

- What is the size and composition of the cafe's customer base?
- How are customers distributed across different age groups?
- Which age group has the largest customer base?
- Which age groups contribute the most offer-associated spending?

### Offer Engagement

- How many offers were received, viewed, and completed?
- How many transactions were associated with an offer?
- Where is the biggest drop-off in the offer journey?

**Offer Received → Offer Viewed → Offer Completed → Offer-Attributed Transaction**

### Transaction Analysis

- What is the total number of transactions?
- How many transactions are offer-associated versus non-offer?
- How does transaction amount differ between offer and non-offer transactions?

### Offer Performance

- How do BOGO and Discount offers compare in terms of transactions?
- How do BOGO and Discount offers compare in terms of transaction amount?
- Which individual offers have better view, completion, and transaction rates?

### Channel Analysis

- Which communication channel or channel combination has the highest transaction rate?
- Which channels have relatively lower transaction rates?

### Customer Segmentation

- How does offer and transaction performance vary by age group, gender, and income group?
- Which customer segments appear to be the most valuable based on offer-associated spending?

---

# 🗂️ Dataset

The project uses three primary datasets:

- `customers.csv` — Customer demographic information
- `offers.csv` — Offer details and attributes
- `events.csv` — Customer-level events such as offer received, offer viewed, offer completed, and transactions

The raw data contained inconsistencies and required transformation before being used for dashboard analysis.

---

# 🧹 Data Cleaning & Transformation

Data preparation was performed using **Power Query in Power BI**.

## Events Table

The Events table contained multiple event types:

- Offer Received
- Offer Viewed
- Offer Completed
- Transaction

The `value` information contained different types of information depending on the event.

Conditional logic was used to separate transaction-related information from offer-related information.

### Key transformations included:

- Separating transaction amount from offer ID information
- Extracting and cleaning offer IDs
- Creating a `clean_offer_id`
- Creating a `final_offer_id`
- Handling transaction events separately from offer events
- Preparing the final Events table for reporting

The resulting `events_final` table became the main analytical event table used for dashboard calculations.

---

# 👥 Customer Data Cleaning

The customer data was cleaned before being integrated with the Events table.

### Customer Age

An `Age` column was created and customers with unrealistic ages above 100 were excluded from the analytical population.

These records did not contain reliable demographic information such as income and gender, so they were removed to avoid misleading customer segmentation and analysis.

### Age Group

An `Age Group` column was created to segment customers into meaningful age categories used in the dashboard.

### Income Band

An `Income Band` column was created to segment customers based on income:

- **Lower Earners:** Income below 40,000
- **Middle Earners:** Income from 40,000 to 80,000
- **Higher Earners:** Income above 80,000

These segments were used for customer-level analysis and dashboard filtering.

---

# 🔗 Data Integration

After cleaning the customer data, customers with valid demographic information were retained.

The cleaned customer table was then merged with the `events_final` table using `customer_id`.

An **Inner Join** was used so that only customers present in both datasets were retained.

This ensured that customers excluded during the customer-data cleaning stage, including customers above the age threshold, did not contribute transactions or offer participation to the final analysis.

The `events_final` table contains the important event-level fields required for reporting, including the cleaned and final offer identifiers.

---

# 📐 Data Model & Data Integration

The project uses `events_final` as the main analytical table.

The original Events data was first transformed and cleaned in Power Query. The transformed data was consolidated into the `events_final` table.

The original `events` and `events_1` tables were used as source/staging tables during the transformation process and were not used as final analytical relationships.

### Final Integration Process

The final `events_final` table was integrated with the cleaned customer and offer information using Power Query merges.

**Customers → events_final**

The Customers table was merged with `events_final` using `customer_id`.

Only customers that passed the customer-data cleaning criteria were included in the final analysis. Customers with unrealistic ages above 100 were excluded before the integration.

**Offers → events_final**

The Offers table was merged with `events_final` using the relevant offer identifier.

This allowed offer attributes such as offer type, reward, duration, and difficulty to be used in the dashboard analysis.

### Final Analytical Table

`events_final` contains the event-level information required for reporting, including:

- Customer ID
- Event type
- Time
- Transaction amount
- Clean Offer ID
- Final Offer ID
- Customer attributes
- Offer attributes

This structure allowed the dashboard to analyze customer behavior, offer engagement, offer performance, and transaction activity from a consolidated analytical table.

---

# 📊 DAX Measures

DAX was used to create business metrics and KPIs for the dashboard.

### Customer & Transaction Measures

- Total Customers
- Total Transactions
- Total Transaction Amount
- Offer Transactions
- Non-Offer Transactions
- Amount from Transactions

### Offer Engagement Measures

- Offer Received
- Offer Viewed
- Offer Completed
- Offer-Attributed Transactions
- View Rate
- Completion Rate
- Transaction Rate through Offer

### Offer & Transaction Analysis

- Offer-Associated Transactions
- Non-Offer Transactions
- Amount from Offer Transactions
- Offer vs. Non-Offer Transaction Analysis
- Offer vs. Non-Offer Amount Analysis

These measures were used to create the dashboard KPIs, charts, funnel analysis, and comparative visuals.

---

# 📊 Dashboard

The Power BI dashboard contains two main analytical pages.

## 1. Overview

The Overview page provides a high-level view of:

- Total Customers
- Total Transactions
- Offer Transactions
- Non-Offer Transactions
- Total Transaction Amount
- Offer engagement funnel
- Offer vs. non-offer transactions
- Offer vs. non-offer transaction amounts
- Offer type performance

## 2. Key Drivers

The Key Drivers page focuses on deeper analysis, including:

- Transaction rate by communication channel
- Offer-associated spending by age group
- Customer distribution by age group
- Offer-level performance
- Reward, duration, difficulty and transaction-rate relationships

---

# 💡 Key Business Insights

### Customer & Transaction Overview

The cleaned dataset contains approximately:

- **14,825 customers**
- **127K total transactions**
- **32K offer-associated transactions**
- **94K non-offer transactions**
- Approximately **1.8M total transaction amount**

Non-offer transactions represent the majority of transaction activity.

### Offer Engagement

The offer funnel shows approximately:

**67K Offers Received → 50K Offers Viewed → 38K Offers Completed → 32K Offer-Attributed Transactions**

The largest drop-off occurs between **Offer Received and Offer Viewed**.

This suggests that improving offer visibility and initial engagement is an important opportunity.

### Offer vs. Non-Offer

Approximately:

- **25.6%** of transactions are offer-associated
- **74.4%** are non-offer

Non-offer transactions also contribute the majority of overall transaction value.

However, offer-associated transactions still represent a meaningful portion of spending.

### Offer Type

Discount offers show stronger transaction activity and transaction amount compared with BOGO offers in the analyzed data.

Informational offers do not show measurable offer-attributed transaction activity in the dashboard analysis.

### Communication Channels

The **Web + Email + Mobile + Social** channel combination shows the highest transaction rate at approximately **65%**.

This indicates that coordinated multi-channel communication can be an important driver of customer engagement.

### Customer Segments

Mature Adults contribute the highest offer-associated spending, followed by:

1. Mature Adults
2. Seniors
3. Adults
4. Young Adults

Mature Adults and Seniors therefore represent important high-value customer segments, while Adults and Young Adults represent potential growth opportunities.

---

# 🚀 Business Recommendations

### 1. Improve Offer Visibility

The largest drop-off occurs between offers being received and viewed.

The cafe should focus on improving offer visibility through better timing, personalization, and communication strategies.

### 2. Prioritize High-Performing Discount Offers

Discount offers show stronger performance in the analyzed data.

The cafe should prioritize successful Discount configurations while continuing to test BOGO offers.

### 3. Target Customer Segments Differently

Mature Adults and Seniors should be retained through relevant and personalized rewards because they currently contribute strongly to offer-associated spending.

Adults and Young Adults should be treated as growth segments and targeted with offers designed to increase engagement.

### 4. Optimize Offer Configuration

Offer performance should be evaluated using a combination of:

**Reward + Duration + Difficulty**

Rather than simply increasing rewards, the cafe should identify configurations that provide an attractive customer proposition while remaining commercially viable.

### 5. Strengthen Multi-Channel Communication

The strongest transaction rate is observed for the Web + Email + Mobile + Social combination.

The cafe should consider coordinated multi-channel campaigns to improve customer engagement.

### 6. Measure Offer Incrementality

Because non-offer transactions represent the majority of transactions, future analysis should investigate whether promotional offers generate incremental spending or are simply associated with purchases customers would have made anyway.

---

# 🤖 AI-Assisted Development & Ethical Use

AI was used throughout this project as a **simulated business stakeholder and analytical mentor**.

AI was used to:

- Help frame the business problem
- Develop and challenge business questions
- Identify potential KPIs
- Discuss data-cleaning approaches
- Review DAX logic
- Discuss analytical approaches
- Help interpret dashboard results
- Challenge potential business conclusions

The Power BI implementation, data preparation, transformation review, dashboard development, result validation, and final business recommendations were reviewed and finalized by me.

AI suggestions were treated as **supporting recommendations rather than automatically accepted outputs**. The analysis was validated against the available data and dashboard results before being included in the final project.

The purpose of using AI was to improve analytical thinking and productivity while maintaining ownership of the implementation, validation, and final conclusions.

---

# 🛠️ Tools & Technologies

- **Power BI**
- **Power Query**
- **DAX**
- **Microsoft Excel / CSV**
- **GitHub**
- **AI-assisted analytical support**

---

# 📁 Repository Structure

```text
Cafe_rewards_powerbi_analytics/
│
├── Business Requirement/
│   └── Business Requirements.pdf
│
├── Documentation/
│   └── Cafe_Rewards_Dashboard_Documentation.pdf
│
├── Insights & Recommendations/
│   └── Business Insights & Recommendations.pdf
│
├── Dashboard/
│   ├── Overview.png
│   └── Key Drivers.png
│
├── Power BI/
│   └── cafe_rewards.pbix
│
├── data/
│   ├── customers.csv
│   ├── events.csv
│   └── offers.csv
│
└── README.md
