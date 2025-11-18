# 🛒 Instacart Market Basket Analysis & Data Model

## 📝 Project Overview

This data engineering project implements a complete **ETL pipeline** to ingest and model the massive **Instacart Online Grocery Shopping Dataset** (3 Million Orders). The goal is to transform the raw CSV files into an optimized **Star Schema** within a **PostgreSQL** database.

The entire process is orchestrated through a **Jupyter Notebook**, utilizing **SQLAlchemy** to manage robust connections, table creation, and data loading. This structured database allows for high-performance **Analytical SQL Queries** to extract business insights, such as market basket analysis and customer behavior trends, which were subsequently executed and analyzed in **PgAdmin**.

---

## ✨ Key Features

* **Dimensional Modeling:** Implemented a **Star Schema** (Fact/Dimension structure) specifically designed for the Instacart dataset for high-performance reporting.
* **Pipeline Automation:** Used **Jupyter Notebook** for end-to-end management, leveraging **SQLAlchemy** for reliable, high-level database interaction.
* **Database Interaction:** Managed database connection, **table creation from scratch**, and bulk data loading into **PostgreSQL** using SQLAlchemy.
* **Complex Analytical Staging:** Utilized a multi-step **temporary table** approach within PostgreSQL to calculate complex metrics (reorder rates, weekday/weekend splits, hourly averages) before combining them into a final analytical table.

---

## 🛠 Technology Stack

| Component | Technology Used | Role in Project |
| :--- | :--- | :--- |
| **Data Source** | **Kaggle: Instacart Dataset** | Raw CSV files containing orders, products, aisles, and departments. |
| **ETL Tool** | **Jupyter Notebook (Python/Pandas)** | Reading CSVs, cleaning data, performing transformations. |
| **DB Connector** | **SQLAlchemy** | **Robust connection management, engine creation, and efficient data loading** into PostgreSQL. |
| **Database** | **PostgreSQL (PgAdmin)** | Data Warehouse for storing the modeled dimensional tables and executing analytical queries. |
| **Analysis** | **SQL** | Analytical querying and analysis within the PgAdmin application. |

---

## 🏗 Data Model & Source Tables

### Source Tables (Raw Data)

The raw data is derived from the following core Instacart dataset tables:

* `Orders Table`
* `Products Table`
* `Order Products Table`
* `Aisles Table`
* `Departments Table`

### Final Analytical Schema

The ETL process creates dimensional tables, and the subsequent SQL analysis culminates in a comprehensive analytical staging table.

| Table Name | Type | Description |
| :--- | :--- | :--- |
| `fact_order_products` | **Fact** | (Created by the ETL process) Contains transactional data linking all dimensions. |
| `dim_products`, `dim_users`, etc. | **Dimensions** | (Created by the ETL process) Descriptive data used in the dimensional model. |
| `final_analysis_table` | **Staging/Analytical** | **(Created by SQL queries)** The final, denormalized table combining all product, department, aisle, and calculated metric information. |

### 🖼 Schema Diagram
A visual representation of the implemented dimensional model is available here:
<img width="729" height="471" alt="ecom_analysis drawio" src="https://github.com/user-attachments/assets/359cc3d9-0c1a-4069-acdd-f073aa417375" />

## 🚀 Getting Started

### 1. Prerequisites

You will need the following installed:

* **Python 3.9+**
* **PostgreSQL** and **PgAdmin**
* **The Instacart Dataset:** Download and extract the raw CSV files into a local directory (e.g., `./data/raw`).

### 2. Installation & Setup

1.  **Clone the repository:**
    ```bash
    git https://github.com/BOSS6292/ETL_Instacart_Analytics.git
    cd ETL_Instacart_Analytics
    ```

2.  **Set up the Python environment:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # Use .\venv\Scripts\activate on Windows
    pip install -r requirements.txt
    ```

3.  **Database Setup:**
    * Ensure your local PostgreSQL server is running.
    * Create a new database (e.g., `instacart_db`) using PgAdmin.
    * **Crucially:** Update the database connection string used by **SQLAlchemy** within the provided **Jupyter Notebook**.

---

## ▶️ Running the Pipeline

The entire ETL process is managed through the notebook.

1.  **Launch Jupyter:**
    ```bash
    jupyter notebook
    ```
2.  **Open the main script:** Navigate to and open the file named `Instacart_ETL_Pipeline.ipynb` (or similar).
3.  **Execute Cells:** Run the cells sequentially. The notebook will:
    * Establish a robust database connection using a **SQLAlchemy Engine**.
    * **Drop and re-create** the dimensional tables (`dim_*` and `fact_*`).
    * Read, clean, and transform the raw CSV data using Pandas.
    * Load the transformed data into the PostgreSQL tables efficiently via SQLAlchemy.

---

## 🔍 SQL Analysis Steps & Results

The final analytical table was constructed through a series of complex SQL queries, utilizing temporary tables (`#temp_...`) for staging intermediate metrics:

1.  **Initial Join Table:** Created a temporary table joining **Orders, Order\_Products, and Products** to establish a base with order, product, department, and aisle information.
2.  **Product Metrics Staging:** Grouped orders by product to calculate the **total purchased count, total reordered count, and average cart position** (`add_to_cart_order`).
3.  **Department Metrics Staging:** Grouped orders by department to calculate the **total purchased, total unique purchased, weekday vs. weekend splits, and average order time of day**.
4.  **Aisle Popularity Staging:** Grouped orders by aisle to find the **Top 10 most popular aisles** based on purchased products and unique product counts.
5.  **Final Combination:** Combined the information from all temporary tables into a definitive `final_analysis_table`, consolidating metrics across product, department, and aisle levels.

### Query Screenshots

Screenshots of the executed analytical SQL queries (including the temporary table creation and the final combination query).
<img width="1920" height="1080" alt="Screenshot (231)" src="https://github.com/user-attachments/assets/24313fef-497a-43f4-ba27-da2c57edde44" />
<img width="1920" height="1080" alt="Screenshot (227)" src="https://github.com/user-attachments/assets/0effe316-a26e-4753-aa80-5e47e5c58b72" />
<img width="1920" height="1080" alt="Screenshot (228)" src="https://github.com/user-attachments/assets/4662f149-e046-4060-84b5-d9f64afac311" />
<img width="1920" height="1080" alt="Screenshot (229)" src="https://github.com/user-attachments/assets/1faa1114-855b-4ea9-8067-eb3c990ac527" />
<img width="1920" height="1080" alt="Screenshot (230)" src="https://github.com/user-attachments/assets/db2b604f-1739-4498-8f19-5fda7a487f2f" />



## 🤝 Contributing

We welcome contributions! Please feel free to open an issue or submit a pull request.

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/new-analysis`)
3.  Commit your Changes (`git commit -m 'Feat: Added new analysis query'`)
4.  Push to the Branch (`git push origin feature/new-analysis`)
5.  Open a Pull Request

---

## 📄 License

Distributed under the **[MIT]** License. See `LICENSE` for more information.

---

## 📧 Contact

Tejas Bomble - tbomble6292@gmail.com

Project Link: https://github.com/BOSS6292/ETL_Instacart_Analytics
