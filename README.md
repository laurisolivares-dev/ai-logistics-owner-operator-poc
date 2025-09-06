# 🚛 Logistic Owner Operator AI – Proof of Concept (POC)

**📌 Project Type:** Proof of Concept (POC)  
**📍 Location:** United States  
**🧠 Focus:** Data Engineering for Logistics  
**🛠️ Technology Stack:** Python · Web Scraping · ETL · Google Cloud Platform · BigQuery · Data Visualization · AI  

---

## 📘 Project Overview

**Logistic Owner Operator AI** is a **Proof of Concept (POC)** focused on **data engineering** for independent trucking professionals in the U.S., using **artificial intelligence** as a transformative tool.

The main goal is to support **owner-operators** in:

- ✅ Validating brokers and dispatchers  
- 💲 Optimizing costs  
- 🛣️ Increasing route efficiency

This analysis focuses on vehicle types such as **Cargo Van, Sprinter Van, Box Truck, and Semi Truck (without dry van)**, with payload capacities ranging from **3,600 lb to 26,000 lb**.

In addition, the project incorporates **payment terms and fees** offered by brokers, as these directly impact the operator’s **liquidity and net profitability**:

- **Same Day Payment** – 5% fee  
- **2–3 Business Days** – 3% fee  
- **14 Business Days** – 0% fee  

This will enable comparison of routes, loads, and brokers not only by gross revenue but also by **net income based on payment timing**.

Rather than defining a single “most profitable” unit, this project aims to **identify under what operational conditions each unit type** (Cargo Van, Sprinter, Box Truck, Semi without dry van) achieves **maximum profitability**.

Although all unit types can be profitable, we seek to understand **how, when, and where** they are — based on variables like **payload, load type, mileage, average route pay, delivery time, operating region, and payment terms**.

---

## 🛠️ Project Goals (POC Data Engineering)

1. 🔍 Validate trustworthy brokers and dispatchers  
2. 📊 Compare profitability by unit type  
3. 💸 Evaluate the impact of payment terms on net revenue  
4. 🛣️ Optimize routes, mileage, and delivery zones  
5. 🤖 Explore AI use for predictive logistics analysis

---

## 💰 Payment Terms Offered by Brokers

Many brokers now offer direct payment options. The following will be analyzed for their **impact on cash flow and true earnings**:

| 💳 Payment Type         | ⏱️ Estimated Time     | 💸 Fee         |
|------------------------|-----------------------|----------------|
| Same Day Payment       | Same day              | 5%             |
| 2–3 Business Days      | 2–3 business days     | 3%             |
| 14 Business Days       | 14 business days      | 0%             |

These terms will be used to calculate **real net revenue** per load.

---

## 📊 Key Analytical Variables

- Vehicle type (van, box truck, etc.)  
- Load weight and dimensions  
- Broker/dispatcher offering the load  
- Operating region or state  
- Route distance (miles)  
- Rate per mile (USD/mile)  
- Payment term and method  
- Estimated delivery time  
- Estimated operational cost (fuel, maintenance, etc.)

---

## 🗂️ Data Sources (Planned)

- Web scraping from broker/freight platforms (e.g., DAT, TruckSmarter)  
- Anonymized real-world load documents  
- Public logistics APIs  
- Structured datasets in Google BigQuery

---

## 📈 Expected Outcomes

- Net profitability comparison by vehicle type and payment method  
- Actionable recommendations for independent carriers  
- Interactive dashboard (Looker Studio or Python) by state, unit, and broker  
- Fully documented and reproducible ETL pipeline  
- Potential future scaling to dry vans and LTL/FTL freight

---

## 🚧 Project Status

- [x] Concept defined (POC)  
- [x] Objectives prioritized  
- [ ] ETL pipeline design  
- [ ] Initial scraper development  
- [ ] Load to BigQuery  
- [ ] Exploratory Data Analysis (EDA)  
- [ ] Visualizations  
- [ ] Final documentation

---

## 🤝 Community Impact

This project is inspired by and dedicated to the U.S. independent trucking community, with whom I share real experiences through a Facebook group. Once complete, the findings will be shared with the group to validate results, gather feedback, and support the growth of the community.

This POC aims to be a useful, realistic, and scalable tool to improve decision-making for owner-operators.

---

## 👩‍💻 Author

**Lauris Olivares** – Data Engineer | SAP Basis Consultant | Owner Operator  
GitHub: [laurisolivares-dev](https://github.com/laurisolivares-dev)  
LinkedIn: [lauris-olivares-06415553](https://linkedin.com/in/lauris-olivares-06415553)
