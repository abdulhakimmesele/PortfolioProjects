# E-commerce Customer Behavior Dataset Cleaning in SQL

# Dataset Overview
This dataset captures detailed information about customer behavior and purchasing patterns, primarily from an e-commerce or retail platform. It includes various features that help in analyzing how customers interact with the site, their purchasing habits, and some demographic details. 

# Introduction
The dataset contains 50 rows and 9 columns. Here are some observations and potential cleaning tasks:

Columns:
Customer ID: Contains customer identifiers, but there are duplicates (e.g., customer 1001 appears multiple times).
Age: Seems okay, though we will check for outliers.
Gender: Likely needs standardization (e.g., capitalization, consistent labeling).
Location: Potential for inconsistent formatting in city names.
Annual Income: No immediate issues, but we will check for outliers or incorrect values.
Purchase History: Contains inconsistent data types (some rows are lists of dictionaries, others are improperly formatted).
Browsing History: Similar to "Purchase History," it has inconsistent formatting.
Product Reviews: Some entries are plain text, while others are dictionaries with ratings.
Time on Site: No immediate issues, but we'll check for outliers.
Cleaning Tasks:
Handle Duplicates: Remove duplicate Customer ID rows by choosing the most recent or relevant entry.
Standardize Text: Clean up gender, location names, and reviews for consistency.
Fix Inconsistent Formats: Reformat the "Purchase History" and "Product Reviews" fields.
Check for Outliers: Identify and handle outliers in Age, Annual Income, and Time on Site.
# Tools I Used
For my deep dive into the data cleaning job , I harnessed the power of several key tools:

- **SQL:** The backbone of my analysis, allowing me to query the database and unearth critical insights.
- **PostgreSQL:** The chosen database management system, ideal for handling the job posting data.
- **Visual Studio Code:** My go-to for database management and executing SQL queries.
- **Git & GitHub:** Essential for version control and sharing my SQL scripts and analysis, ensuring collaboration and project tracking.
# Cleaning the data
### 1.  Remove Duplicate Customer ID
Keep only the entry with the highest Time on Site for each customer.
```sql
DELETE FROM ecommerce_table
WHERE (CustomerID, TimeOnSite) NOT IN (
    SELECT CustomerID, MAX(TimeOnSite)
    FROM ecommerce_table
    GROUP BY CustomerID
);
```
### 2. Standardize Gender Field
Convert all gender values to proper case (capitalize the first letter).
```sql
UPDATE ecommerce_table
SET Gender = CONCAT(UPPER(SUBSTRING(Gender, 1, 1)), LOWER(SUBSTRING(Gender, 2)));
```
### 3. Standardize Location Field
Trim spaces and capitalize each word in the Location field.
```sql
UPDATE ecommerce_table
SET Location = INITCAP(TRIM(Location));
```
### 4. Handle Outliers in Age, Annual Income, and Time on Site
Remove rows where age is outside the reasonable range (e.g., less than 18 or more than 100) and remove rows with unrealistic income or site times.
```sql
DELETE FROM ecommerce_table
WHERE Age < 18 OR Age > 100;

DELETE FROM ecommerce_table
WHERE AnnualIncome < 10000 OR AnnualIncome > 500000;

DELETE FROM ecommerce_table
WHERE TimeOnSite > 1000;
```
### 5. Format Purchase History and Browsing History
For cleaning JSON-like data in SQL (depending on your SQL engine), you may want to store Purchase History and Browsing History as proper JSON fields and parse them.

If the data is stored as a string and you want to parse it into a JSON column:
```sql
ALTER TABLE ecommerce_table
ADD COLUMN PurchaseHistoryJSON JSON;

UPDATE ecommerce_table
SET PurchaseHistoryJSON = JSON(PurchaseHistory);
```
### 6. Format Product Reviews
Similar to Purchase History, format Product Reviews into structured JSON data.
```sql
ALTER TABLE ecommerce_table
ADD COLUMN ProductReviewsJSON JSON;

UPDATE ecommerce_table
SET ProductReviewsJSON = JSON(ProductReviews);
```
### Key Changes:

- **Duplicate Customer ID entries are removed.**
- **Standardized Gender and Location columns.**
- **Removed outliers in Age, Annual Income, and Time on Site.**
- **Reformatted Purchase History, Browsing History, and Product Reviews into structured JSON format.**

  This cleaned dataset is now ready for further analysis, such as SQL queries, visualization, or machine learning. 
