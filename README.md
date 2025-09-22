# 🚛 Logistic Owner Operator AI – Proof of Concept (POC)

**📌 Project Type:** Proof of Concept (POC)  
**📍 Location:** United States  
**🧠 Focus:** Data Engineering for Logistics  
**🛠️ Technology Stack:** Python · Web Scraping · ETL · Google Cloud Platform · BigQuery · Data Visualization · AI  

---

## 📘 Project Overview

**Logistic Owner Operator AI** is a **Proof of Concept (POC)** focused on **data engineering** for independent trucking professionals in the U.S., using **artificial intelligence** as a transformative tool.

The main goal is to support **owner-operators** in:

- ✅ Validating brokers and dispatchers.  
- 💲 Optimizing costs.  
- 🛣️ Increasing route efficiency.

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

1. 🔍 Validate trustworthy brokers and dispatchers.  
2. 📊 Compare profitability by unit type.  
3. 💸 Evaluate the impact of payment terms on net revenue.  
4. 🛣️ Optimize routes, mileage, and delivery zones.  
5. 🤖 Explore AI use for predictive logistics analysis.

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

- Vehicle type (van, box truck, etc.).  
- Load weight and dimensions.  
- Broker/dispatcher offering the load.  
- Operating region or state.  
- Route distance (miles).  
- Rate per mile (USD/mile).  
- Payment term and method.  
- Estimated delivery time.  
- Estimated operational cost (fuel, maintenance, etc.).

---

## 🗂️ Data Sources (Planned)

- Web scraping from broker/freight platforms (e.g., DAT, TruckSmarter).  
- Anonymized real-world load documents.  
- Public logistics APIs.  
- Structured datasets in Google BigQuery.

---
## 🧱 Web Scraper Phases

### ✅ Phase 1: Structured Block-Based Extraction

In this first phase, we developed a **modular thematic scraper** focused on the **structured extraction of critical data blocks** from the public SAFER FMCSA page, using the **MC Number** as the primary identifier.

🔍 **Main Goal:**  
Retrieve key compliance, operational, and safety data for registered carriers/brokers in the U.S. Department of Transportation (USDOT) system, organized by logical sections.

📦 **Extracted Blocks:**

- 🆔 **Entity Identification:**  
  - Legal Name, DBA Name.  
  - USDOT Number, MC Number.  
  - Physical Address, Mailing Address, Phone.

- 🏢 **Registration Information:**  
  - Entity Type.  
  - USDOT Status.  
  - Operating Authority Status.

- ⚙️ **Operational Classification:**  
  - Operation Classification.  
  - Carrier Operation.

- 📊 **Compliance & Inspections:**  
  - Inspection counts (Vehicle, Driver, Hazmat, IEP).  
  - Out-of-Service % (OOS).  
  - Comparison with national average.

- 🚧 **Crash History:**  
  - Number of incidents (Fatal, Injury, Tow, Total).

- 📋 **Carrier Safety Rating:**  
  - Rating Date, Review Date, Rating, Type.

🛠 **Techniques Used:**

- `Requests` to fetch public HTML content. 
- `BeautifulSoup` to parse the DOM structure.  
- Robust table parsing via `<td>` and class targeting.  
- Clean data aggregation into structured dictionary blocks.  
- JSON export for future use in Data Lakes or ETL pipelines.

✅ This structure enables easy extension of the scraper in future stages, including multi-MC automation, error handling, bulk scraping, and cloud-based storage in BigQuery or Cloud Storage.

---

## 🧩 Stage 2: JSON Storage for Extracted MC Data

In this stage, we implemented the logic to **store all extracted blocks from the FMCSA SAFER website into structured JSON files**, organized by each MC number.

### 🔸 Purpose:
Enable persistent storage of all extracted data (USDOT info, Company Info, Inspections, Crashes, etc.) per MC number, to support future querying, analysis, and integration into cloud ETL pipelines.

### 🛠️ Implementation Details:

- A Python dictionary is dynamically built during the parsing phase.
- Each section is stored as a key-value block (e.g., `"USDOT Information"`, `"Crash History"`, `"Carrier Safety Rating"`).
- The data is saved in `.json` format using Python's built-in `json.dump()` function.

### 📁 JSON Output Sample:
File saved as:
```bash
outputs/MC_1498383.json

{
  "USDOT Information": {
    "Entity Type": "CARRIER",
    "USDOT Status": "ACTIVE",
    "USDOT Number": "3992838",
    "MCS-150 Form Date": "01/19/2025",
    "Out of Service Date": "None",
    "State Carrier ID Number": "N/A",
    "MCS-150 Mileage (Year)": "N/A"
  },
  "Operating Authority Status": "AUTHORIZED FOR Property For Licensing and Insurance details click here.",
  "Company Information": {
    "Legal Name": "MYDELIVERYS919 LLC",
    "DBA Name": "",
    "Physical Address": "8226 ROLLINGHITCH CT MAINEVILLE, OH 45039",
    "Mailing Address": "8226 ROLLINGHITCH CT MAINEVILLE, OH 45039",
    "Phone": "(513) 828-7166",
    "DUNS Number": "--",
    "Power Units": "0",
    "Non-CMV Units": "1",
    "Drivers": "1"
  },
  "Operation Classification": [
    "Auth. For Hire",
    "Interstate",
    "General Freight",
    "Metal: sheets, coils, rolls",
    "Building Materials",
    "Utilities"
  ],
  "Carrier Operation": "Interstate",
  "Inspections Summary": {
    "Inspections": {
      "Vehicle": "0",
      "Driver": "0",
      "Hazmat": "0",
      "IEP": "0"
    },
    "Out of Service": {
      "Vehicle": "0",
      "Driver": "0",
      "Hazmat": "0",
      "IEP": "0"
    },
    "Out of Service %": {
      "Vehicle": "0%",
      "Driver": "0%",
      "Hazmat": "0%",
      "IEP": "0%"
    },
    "Natl Avg %": {
      "Vehicle": "22.26%",
      "Driver": "6.67%",
      "Hazmat": "4.44%",
      "IEP": "N/A"
    }
  },
  "Crash History": {
    "Fatal": "0",
    "Injury": "0",
    "Tow": "0",
    "Total": "0"
  },
  "Carrier Safety Rating": {
    "Rating Date": "None",
    "Review Date": "None",
    "Rating": "None",
    "Type": "None"
  }
}
```

**📁 Location of generated JSON files:**
All files are stored in the `outputs/` folder in your local environment, for example:
`C:\outputs\MC_1498383.json`

**💡 Benefit:**
This structure allows for subsequent queries, integration with ETL pipelines, comparative analysis between MCs, or visualization in external dashboards.

---
### 🔍 Technical Challenges and Solutions Applied

During this first stage of development, we encountered and overcame several key challenges in building a robust and accurate scraper:

#### 🧱 1. DOM-based Navigation and Inconsistent Structure
- **Challenge**: The HTML structure of the FMCSA (SAFER) portal varies subtly between different MC profiles.
- **Solution**: We designed modular block-based extractors (USDOT Info, Company Info, Classification, Inspections, etc.) using `BeautifulSoup` and a `<th>`-based regex approach. This allowed data extraction even when labels and values were not consistently aligned.

#### ⏱️ 2. Timing and Page Load Delays
- **Challenge**: The page does not load instantly; some tables take a few seconds to fully render.
- **Solution**: We implemented `WebDriverWait` with explicit conditions (`EC.presence_of_element_located`) to ensure the DOM was fully loaded before parsing with BeautifulSoup.

#### ⚠️ 3. Navigation Errors or Missing Data
- **Challenge**: Some MC numbers return incomplete data or fail to load entirely.
- **Solution**: We added `try/except` blocks and content validation with `if not soup.find(...)`, allowing graceful error handling without crashing the scraper.

#### 🧩 4. Modularity and Helper Functions
- **Challenge**: Repetition of patterns in similar data extraction tasks.
- **Solution**: We created helper functions (`get_value_by_label`, `get_address_block`, `extract_table_data`, etc.) to reduce code duplication and improve clarity. This supports a scalable block-based architecture.

#### 🔒 5. Session Closing and Resource Cleanup
- **Challenge**: WebDriver may leave background processes open if not properly handled.
- **Solution**: We added a clean shutdown with `driver.quit()` and used a `try/finally` block to prevent memory leaks or orphaned browser instances.

---
### 📦 Technical Summary of Stage 2

Unlike Stage 1, this phase did not present major technical difficulties. Thanks to the modular block-based architecture created earlier (`extract_usdot_information`, `extract_company_information`, `extract_classifications`, etc.), we successfully aggregated all data into a unified dictionary and exported it to a `.json` file.

#### ✅ Accomplishments:

- Structured data collection by thematic blocks (USDOT Info, Company Info, Classifications, Inspections, Crash, Rating).
- Assembled a single structured dictionary (`carrier_data`) with descriptive keys.
- Included the MC number as a unique identifier in the file name.
- Exported using `json.dump()` with `indent=4` for enhanced readability and validation.
- Files are automatically saved to the `/outputs/` directory, for example:

```json
📁 outputs/MC_1498383.json

---

✨ Thanks to these solutions, we built a **solid, modular, and resilient Stage 1**, capable of adapting to a wide variety of FMCSA profile structures.

---
## 📈 Expected Outcomes

- Net profitability comparison by vehicle type and payment method.  
- Actionable recommendations for independent carriers.  
- Interactive dashboard (Looker Studio or Python) by state, unit, and broker.  
- Fully documented and reproducible ETL pipeline.  
- Potential future scaling to dry vans and LTL/FTL freight.

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
