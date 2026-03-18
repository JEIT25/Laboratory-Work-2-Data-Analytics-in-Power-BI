# Laboratory Work 2 - End-to-End Data Analytics in Power BI: From Data Cleaning to DAX Insights

## 🎯 Lab Objectives
* Clean and prepare raw datasets for analysis.
* Apply data transformation techniques using Power Query.

## 📁 Dataset
* `Messy_Sales_Data.xlsx` 

---

## 🛠️ Laboratory Activities (Methodology)

### Part 1: Open Power Query Editor
1. Opened Power BI Desktop.
2. Navigated to **Home** → **Get Data** → **Excel/CSV Workbook**.
3. Loaded the messy sales dataset.
4. Clicked **Transform Data** to open the Power Query Editor.

### Part 2: Remove Duplicates
1. Selected the primary table.
2. Highlighted the `OrderID` column as the unique identifier.
3. Navigated to **Home** → **Remove Rows** → **Remove Duplicates**.

### Part 3: Handle Missing Values
Identified columns with `null` or empty string values and applied the following transformations:
* **Quantity:** Replaced missing/null values with `0` (**Transform** → **Replace Values**).
* **Region:** Converted hidden empty strings to true `null` values, then applied **Transform** → **Fill** → **Down** to carry categorical data forward.
* **Blank Rows:** Removed entirely via **Remove Rows** → **Remove Blank Rows**.

### Part 4: Change Data Types
Evaluated the icons beside column names and standardized the types to ensure accurate DAX calculations:
* **Date:** Changed to `Date` type (Required handling of mixed international/US date formats and text-based dates).
* **Sales:** Changed to `Decimal Number` (Required stripping hidden quotation marks, e.g., `"7500"`).
* **Quantity:** Changed to `Whole Number`.

### Part 5: Rename Columns Properly
Standardized column naming conventions for readability and DAX integration:
* `order_id`
* `order_date`
* `customer_name`
* `total_sales` (mapped from `SalesAmount`)

---

## 📦 Student Deliverables

- [x] Cleaned dataset successfully loaded into Power BI.
- [x] Screenshot of the Applied Steps pane.

> **Note to Reviewer:** Insert the required screenshot of the Power Query 'Applied Steps' pane below.
> 
> ![Applied Steps Pane](./path_to_your_screenshot/applied_steps.png)

---

## 📝 Guide Questions & Answers

**1. Why is removing duplicates important in data analysis?**
Removing duplicates ensures data integrity. If duplicate rows exist, metrics like Total Sales or Total Orders will be artificially inflated, leading to inaccurate insights and poor business decisions.

**2. What problems can missing values cause in reports?**
Missing values (nulls or blanks) can cause visual charts to generate a "(Blank)" category, skew average calculations (since the denominator might change), and cause errors when creating standard DAX formulas.

**3. How does correct data typing affect calculations?**
Power BI's calculation engine relies on data types. If a number (like Sales) is stored as text (e.g., `"7500"`), Power BI cannot sum or average it. If a Date is stored as text, Time Intelligence functions (like Year-over-Year growth or Monthly comparisons) will fail to work entirely.

**4. What naming conventions improve data readability?**
Using consistent conventions like `snake_case` (e.g., `order_date`) or `Title Case` with spaces (e.g., `Order Date`) makes DAX formulas easier to write and read. It also ensures that the auto-generated axis titles on charts look clean and professional without requiring manual overrides.

---

## 🚀 Enhancement Activities

### Data Quality Checklist for Future Datasets
1. **Uniqueness:** Are there duplicate primary keys (e.g., Order IDs)?
2. **Completeness:** Are there nulls or blanks in critical columns?
3. **Consistency:** Do dates follow a single, standardized format (e.g., YYYY-MM-DD)?
4. **Validity:** Are numerical columns free of text characters, spaces, or symbols (like quotes or currency signs)?
5. **Formatting:** Are column names standardized and descriptive?

### Dataset Size Comparison
* **Before Cleaning:** 500 rows, unstructured formatting, mixed data types, and missing fields.
* **After Cleaning:** Reduced row count (due to duplicate/blank removal), 100% typed columns, and fully populated categorical columns (via fill-down). 

### Research: What is ETL and how does Power Query support it?
**ETL** stands for **Extract, Transform, and Load**, which is the core process of data integration:
* **Extract:** Pulling data from raw sources (Excel, CSV, SQL databases).
* **Transform:** Cleaning the data (removing duplicates, handling nulls, changing types).
* **Load:** Pushing the clean data into a destination system (the Power BI Data Model).
**Power Query** supports ETL by providing a visual interface to perform the "Transform" step while recording every action in the "Applied Steps" pane. This creates a repeatable ETL pipeline, meaning the data cleans itself automatically upon the next refresh.
