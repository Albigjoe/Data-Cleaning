Comprehensive Data Cleaning Process for Gllassdoor data Job Dataset
1. Identifying & Removing Duplicate Entries
•	I used ROW_NUMBER()windows function to check for duplicate and remove duplicates 
2. Cleaning Text-Based Columns
•	Job Titles: Using replace function to removed unnecessary characters like parentheses, dashes, and numbers (e.g., (Sr.) → Sr).
•	Salary Estimates: Removed extra text such as "(Glassdoor est.)" and "(Employer est.)" to retain only salary numbers. I used string_split
•	Company Names: Stripped out trailing numbers (e.g., Company123 → Company).
•	Invalid Values: Set NULL for Headquarters, Founded, Revenue, Size, and Sector where values were -1 or Unknown.
3. Splitting Salary Estimates
•	Salary values were stored as ranges (e.g., "50k-70k"), so we:
o	I Used STRING_SPLIT() to separate the minimum and maximum salary.
o	Created MIN_SAL and MAX_SAL columns.
o	Calculated Average Salary as (MIN_SAL + MAX_SAL) / 2.
4. Standardizing Company Size
•	Removed unnecessary words like "employees", "to", and "+" from size descriptions.
using replace function 
•	Split Size into min_sizes and max_sizes using STRING_SPLIT().
•	Calculated avg_sizes to estimate company workforce.
5. Cleaning & Structuring Revenue Data
•	Revenue was given as ranges (e.g., "1-5 billion" or "500 million+").
•	Extracted min_revenue and max_revenue by:
•	Identifying if the unit was "million" or "billion"..(This was hard for me had to ask ai for help I could split it 
the problem was getting the min column to take the billion unit and not only thr max column)
o	
o	Converting values to numerical format (billion → * 1,000,000,000, million → * 1,000,000).
o	Handling missing values: If max_revenue was missing (+ sign cases), only min_revenue was stored.
•	Calculated avg_rev as (min_revenue + max_revenue) / 2, ensuring no division errors when one value was missing6. Handling Missing Data
•	Set NULL values for empty Location fields.
•	Removed Competitors column and added a cleaned Competitor column.
7. Finalizing the Cleaned Dataset
•	Dropped unnecessary columns like Job Description, Revenue, and Competitors.
•	Performed a final SELECT to verify the cleaned data.

