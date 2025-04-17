
# 📊 Project-Based Internship Program - Kimia Farma Big Data Analytics

## 📌 Program Description

This project is part of a **Project-Based Internship Program** in collaboration between **Rakamin Academy** and **Kimia Farma**, focusing on **Big Data Analytics**. The program aims to enhance participants' understanding and skills as Big Data Analysts in a real-world business environment.

Throughout the internship, participants received:
- Learning materials (videos and articles) from industry practitioners
- Weekly tasks to assess understanding of each module
- A final project to analyze business performance using real datasets and build a professional portfolio

---

## 🏢 About Kimia Farma

**Kimia Farma** is the first pharmaceutical company in Indonesia, established in 1817 during the Dutch colonial era under the name **NV Chemicalien Handle Rathkamp & Co**. The company was nationalized in 1958 as PNF Bhinneka Kimia Farma, and later transformed into PT Kimia Farma (Persero) in 1971. Today, Kimia Farma is one of the key players in the national pharmaceutical industry.

---

## 🎯 Project Objectives

The project aims to:
- Evaluate **Kimia Farma's business performance** from 2020 to 2023
- Analyze transactional, product, branch, and inventory data
- Build an **interactive dashboard** using **Google Looker Studio** to visualize key performance indicators

---

## 🧰 Technologies Used

- **Google BigQuery** – for data warehousing and querying
- **SQL** – for data processing and analysis
- **Google Looker Studio** – for dashboard creation and data visualization

---

## 📂 Datasets

The following datasets were used:
1. `kf_final_transaction` – Final transaction data
2. `kf_inventory` – Inventory data
3. `kf_kantor_cabang` – Branch office information
4. `kf_product` – Product details
5. 'kimia_farma_analysis' - Merged dataset
   
🔗 [Link dataset](https://drive.google.com/drive/folders/1NzBk0OemXnXI0PkCYcoVNJdBuVkXYDBC?usp=sharing)
   

---

## 🛠️ Process & Challenges

### ✅ Challenge 1: Import Datasets to BigQuery

Imported four datasets into Google BigQuery for further processing and analysis.

---

### ✅ Challenge 2: Create Analysis Table

A combined table called `kimia_farma_analysis` was created by joining transaction, branch, and product data, along with calculated fields such as net sales and net profit.

#### SQL Query Used:

```sql
CREATE OR REPLACE TABLE ascendant-ridge-454416-m4.kimia_farma.kimia_farma_analysis AS
SELECT 
    t.transaction_id,
    t.date,
    c.branch_id,
    c.branch_name,
    c.kota,
    c.provinsi,
    c.rating AS rating_cabang, 
    t.customer_name,
    p.product_id,
    p.product_name,
    t.price AS actual_price, 
    t.discount_percentage,
    (t.price - (t.price * t.discount_percentage / 100)) AS nett_sales,
    CASE 
        WHEN t.price <= 50000 THEN 0.10
        WHEN t.price > 50000 AND t.price <= 100000 THEN 0.15
        WHEN t.price > 100000 AND t.price <= 300000 THEN 0.20
        WHEN t.price > 300000 AND t.price <= 500000 THEN 0.25
        ELSE 0.30
    END AS persentase_gross_laba,
    ((t.price - (t.price * t.discount_percentage / 100)) * 
    CASE 
        WHEN t.price <= 50000 THEN 0.10
        WHEN t.price > 50000 AND t.price <= 100000 THEN 0.15
        WHEN t.price > 100000 AND t.price <= 300000 THEN 0.20
        WHEN t.price > 300000 AND t.price <= 500000 THEN 0.25
        ELSE 0.30
    END) AS nett_profit,
    t.rating AS rating_transaksi
FROM ascendant-ridge-454416-m4.kimia_farma.kf_final_transaction t
JOIN ascendant-ridge-454416-m4.kimia_farma.kf_kantor_cabang c 
  ON t.branch_id = c.branch_id
JOIN ascendant-ridge-454416-m4.kimia_farma.kf_product p 
  ON t.product_id = p.product_id;
```

**Explanation:**
- Combines three datasets (`transaction`, `branch`, and `product`)
- Calculates **net sales** (after discount)
- Applies **gross profit percentage** using `CASE` logic
- Computes **net profit** based on net sales and profit margin
- Also includes customer and transaction rating for performance insights

---

### ✅ Challenge 3: Build Dashboard in Looker Studio

An interactive dashboard was built with the following insights:
-  Total Revenue & Transaction Trends
-  Transaction Distribution by Province
-  Top 10 Net Sales by Branch/Province
-  Average Customer Rating
-  High-rated Branches with Low Transactions
-  Profit Distribution across Regions



---
### 📈 Performance Insights

- **Annual Revenue Performance (2020–2023):**  
  Kimia Farma's annual net sales remained stable between **IDR 86–87 billion**, with no significant spikes or drops throughout the period.

- **Overall Sales Performance:**  
  - Total Revenue: IDR 346.96 billion  
  - Total Transactions: 672,458  
  - Total Customers: 264,601  

- **Average Customer Satisfaction:**  
  The average rating across all branches is **4 out of 5**, indicating high satisfaction.

- **High-Rating, Low-Transaction Branches:**  
  Branches like **Sorong, Cikampek, Kupang, Samarinda**, and **Pematangsiantar** show high ratings but low transactions — a sign of **untapped potential**.

- **Geographic Distribution of Transactions:**  
  Most transactions occur in **West Java**, followed by **North Sumatra** and **Central Java**.

- **Top Provinces by Net Sales Contribution:**  
  - West Java  
  - North Sumatra  
  - Central Java  
  - East Java  

- **Top Provinces by Transaction Volume:**  
  - West Java: 198.7k  
  - North Sumatra: 48.2k  
  - Central Java: 46.5k  

---

## ✅ Recommendations

### Enhance Performance of Branches with High Ratings but Low Transactions  
→ Run **localized marketing campaigns** or optimize sales strategies to increase transaction volume in branches like **Sorong** and **Kupang**.

### Maintain and Optimize High-Performing Branches  
→ Focus on branches in **West Java** and other top-performing provinces by ensuring **product availability**, **adequate staffing**, and **consistent service quality**.

### Expand in Provinces with High Profit Margins  
→ Allocate more resources to regions with **high net profit margins** to **scale operations** and **replicate success**.

---
## 📊 Dashboard

<p align="center">
  <a href="https://lookerstudio.google.com/reporting/e655d103-a261-4f18-928e-0f284a30312f" target="_blank">
    <img src="https://github.com/user-attachments/assets/60312d98-7b54-46df-b18b-b81927ac9acf" alt="Dashboard Preview" width="800">
  </a>
</p>

🔗 [View Full Dashboard on Looker Studio](https://lookerstudio.google.com/reporting/e655d103-a261-4f18-928e-0f284a30312f)

---
## 👤 Author


**Yusep Fathul Anwar**  
Big Data Analytics Intern – Rakamin x Kimia Farma

---


