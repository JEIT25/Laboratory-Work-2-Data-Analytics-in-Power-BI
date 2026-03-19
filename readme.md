# Laboratory Work 2 - End-to-End Data Analytics in Power BI: From Data Cleaning to DAX Insights

## 🎯 Lab Objectives
* Clean and prepare raw datasets for analysis.
* Apply data transformation techniques using Power Query.
* Integrate multiple datasets using Merge and Append functions.

## 📁 Datasets
* `Messy_Sales_Data.xlsx` (Cleaned into `Fixed_Dates_Only.csv`)
* `Orders.csv`, `Customers.csv`
* `Sales_January.csv`, `Sales_February.csv`, `Sales_March.csv`

---

## 🛠️ Section 1: Data Cleaning (Methodology)

### Part 1: Open Power Query Editor
1. Opened Power BI Desktop and navigated to **Get Data**.
2. Loaded the messy sales dataset and opened the Power Query Editor.

### Part 2: Remove Duplicates
1. Highlighted the `OrderID` column as the unique identifier.
2. Navigated to **Home** → **Remove Rows** → **Remove Duplicates**.

### Part 3: Handle Missing Values
* **Quantity:** Replaced `null` values with `0`.
* **Region:** Converted empty strings to true `null` values, then applied **Fill Down** to carry categorical data forward.

### Part 4: Change Data Types
* **Date:** Changed to `Date` type (resolved complex mixed-format date errors).
* **Sales:** Changed to `Decimal Number` (stripped hidden text quotation marks).
* **Quantity:** Changed to `Whole Number`.

### Part 5: Rename Columns Properly
Standardized naming conventions: `order_id`, `order_date`, `customer_name`, `total_sales`.

> **Cleaned Data Deliverables:**
> ![Cleaned Dataset Part 1](./screenshot_outputs/clean_dataset1.png)
> ![Cleaned Dataset Part 2](./screenshot_outputs/clean_dataset2.png)
> ![Cleaned Dataset Part 3](./screenshot_outputs/clean_dataset3.png)
> ![Applied Steps Pane](./screenshot_outputs/cleaning_applied_steps.png)

---

## 🔗 Section 2: Merge and Append Queries (Methodology)

### Part 1: Merge Queries (Inner Join)
1. Loaded `Orders.csv` and `Customers.csv`.
2. Promoted headers in `Customers.csv` using **Use First Row as Headers**.
3. Selected the `Orders` query, clicked **Merge Queries**.
4. Selected the `Customers` table to merge with, matching them via the `Customer ID` column.
5. Selected **Inner (only matching rows)** as the Join Kind.
6. Expanded the newly merged table to extract `Customer Name`, `Segment`, and `Country`.

> **Merge Deliverables:**
> ![Merge Dialog](./screenshot_outputs/image_4ddd00.png)
> ![Expanded Columns](./screenshot_outputs/image_4de0a3.png)

### Part 2: Append Monthly Sales Files
1. Loaded `Sales_January.csv`, `Sales_February.csv`, and `Sales_March.csv`.
2. Ensured all three tables had matching column headers by promoting the first row to headers in January.
3. Selected `Sales_January` and clicked **Append Queries as New**.
4. Selected **Three or more tables** and added February and March to the list.
5. Named the new combined query `All_Q1_Sales`.

> **Append Deliverables:**
> ![Append Dialog](./screenshot_outputs/image_4de03e.png)
> ![Appended Result](./screenshot_outputs/image_4de388.png)

---

## 📝 Guide Questions & Answers

### Data Cleaning Questions
**1. Why is removing duplicates important in data analysis?**
Removing duplicates ensures data integrity. If duplicate rows exist, metrics like Total Sales will be artificially inflated.

**2. What problems can missing values cause in reports?**
Missing values cause visual charts to generate a "(Blank)" category, skew average calculations, and cause DAX formula errors.

**3. How does correct data typing affect calculations?**
Power BI's calculation engine relies on data types. If a number is stored as text, Power BI cannot sum it. If a Date is stored as text, Time Intelligence functions will fail.

**4. What naming conventions improve data readability?**
Using consistent conventions like `snake_case` (e.g., `order_date`) makes DAX formulas easier to write and ensures auto-generated chart titles look clean.

### Merge and Append Questions
**1. What is the difference between Merge and Append in Power Query?**
* **Merge** adds columns horizontally. It is like a SQL `JOIN`, combining two different tables based on a shared/common key (e.g., Customer ID).
* **Append** adds rows vertically. It is like a SQL `UNION`, stacking tables with the exact same columns on top of each other (e.g., stacking months of sales).

**2. Why use an Inner Join instead of a Left Outer Join in this scenario?**
An Inner Join strictly keeps only the records where a matching Customer ID exists in both the Orders and Customers tables. This filters out "orphaned" orders that lack customer details, ensuring our sales analysis is only based on fully verified customer data.

**3. How does appending monthly files improve scalability?**
Appending allows you to create a scalable pipeline. Instead of manually copying and pasting data in Excel every month to create one massive file, you simply drop the new month's CSV into Power BI and append it. It automates the consolidation process.

---

## 🚀 Enhancement Activities

### Observation: Left Outer vs. Inner Join
If the join type is changed to a **Left Outer Join**, the query keeps *all* rows from the first (Orders) table, even if the Customer ID doesn't exist in the Customers table. The result is that orphaned orders remain in the dataset, but the expanded columns (`Customer Name`, `Segment`, `Country`) will show up as `null` (blank) for those specific records.

### Research: Power BI Maximum Row Capacity
Power BI does not have a strict "row limit" like Excel's 1,048,576 rows. Instead, it is limited by memory/file size:
* **Power BI Pro (Desktop):** Limited to a 1 GB dataset size, which, thanks to Power BI's VertiPaq compression engine, can easily hold tens to hundreds of millions of rows depending on the number of columns and data cardinality.
* **Power BI Premium:** Can handle massive enterprise datasets up to 400 GB in memory, effectively processing billions of rows.
