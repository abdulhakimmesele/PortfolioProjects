# PortfolioProjects
projects uses for data analysis

About the Data Set file:-
This dataset captures detailed information about customer behavior and purchasing patterns, primarily from an e-commerce or retail platform. It includes various features that help in analyzing how customers interact with the site, their purchasing habits, and some demographic details. 

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
I will start by addressing duplicates and then move on to standardizing and fixing inconsistent formats. 
