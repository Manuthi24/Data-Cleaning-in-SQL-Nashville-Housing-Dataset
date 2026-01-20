# 🏠 Nashville Housing Data Cleaning Project (SQL)

## 📌 Project Overview
This project focuses on **cleaning and transforming raw housing data** into a format that is more usable and analysis-friendly.  
Data cleaning is a critical responsibility of a **Data Analyst**, often consuming the majority of a project’s timeline.

Using **Microsoft SQL Server**, I performed a series of **advanced data cleaning operations**, including standardising date formats, handling missing values, splitting concatenated fields, ensuring data consistency, and removing duplicate records.

---

## 📂 Dataset
The dataset used in this project is **Nashville Housing Data for Data Cleaning**, containing approximately **56,000 housing records**.

### Key Columns:
- `UniqueID`, `ParcelID`
- `PropertyAddress`, `OwnerAddress`
- `SaleDate`, `SalePrice`
- Land value, number of bedrooms, and bathrooms

---

## 🛠 Tools & Technologies
- **SQL Server Management Studio (SSMS)**
- **Microsoft SQL Server 2019 Import & Export Wizard**
- **T-SQL (Transact-SQL)**

---

## 🧹 Data Cleaning Steps

### 1️⃣ Standardise Date Format
The original `SaleDate` column contained unnecessary time components.

- **Action:** Converted `SaleDate` to a standard `DATE` format.
- **Technical Approach:**  
  - Added a new column `SaleDateConverted`
  - Populated it using `CONVERT(Date, SaleDate)` to ensure consistency where direct updates failed

---

### 2️⃣ Populate Missing Property Address Data
Some rows contained `NULL` values in the `PropertyAddress` column.

- **Action:** Filled missing addresses using existing records with the same `ParcelID`
- **Technical Approach:**  
  - Performed a **Self-Join** on `ParcelID`
  - Used `ISNULL()` to populate missing values from matching records with different `UniqueID`s

---

### 3️⃣ Split Address Fields into Individual Columns
Addresses were stored as single concatenated strings, limiting usability for analysis.

#### Property Address
- Split into **Address** and **City**
- Used `SUBSTRING` and `CHARINDEX` with a comma delimiter

#### Owner Address
- Split into **Address**, **City**, and **State**
- Used `REPLACE` to convert commas into periods
- Extracted components using `PARSENAME`

---

### 4️⃣ Standardise SoldAsVacant Values
The `SoldAsVacant` column contained inconsistent values (`Y`, `N`, `Yes`, `No`).

- **Action:** Standardised all values to `Yes` and `No`
- **Technical Approach:** Used a `CASE` statement

---

### 5️⃣ Remove Duplicate Records
Duplicate records can distort analysis and lead to incorrect insights.

- **Action:** Identified and removed duplicates
- **Technical Approach:**  
  - Created a **CTE** using `ROW_NUMBER()`
  - Partitioned by:
    - `ParcelID`
    - `PropertyAddress`
    - `SalePrice`
    - `SaleDate`
    - `LegalReference`
  - Deleted rows where `ROW_NUMBER > 1`

---

### 6️⃣ Delete Unused Columns
After creating cleaner, more structured columns, redundant fields were removed.

- **Action:** Dropped unnecessary columns such as:
  - `OwnerAddress`
  - `TaxDistrict`
  - Original `PropertyAddress`
- **Technical Approach:** Used `ALTER TABLE ... DROP COLUMN`

---

## 🧠 Key SQL Concepts Demonstrated
- **Joins:** Self-Joins for data population  
- **Window Functions:** `ROW_NUMBER()` with `PARTITION BY`  
- **CTEs:** Simplifying complex queries and duplicate removal  
- **String Manipulation:** `SUBSTRING`, `CHARINDEX`, `PARSENAME`, `REPLACE`  
- **Conditional Logic:** `CASE` statements  
- **DDL & DML:** `ALTER TABLE`, `UPDATE`, `DELETE`, `SET`

---

## 🎯 Project Outcome
- Converted raw housing data into a **clean, structured, and analysis-ready dataset**
- Improved **data consistency, usability, and reliability**
- Demonstrated real-world **SQL data cleaning techniques** used by data analysts

---


<p align="center">
  <em>Clean data is the foundation of meaningful analysis and confident decision-making.</em>
</p>

