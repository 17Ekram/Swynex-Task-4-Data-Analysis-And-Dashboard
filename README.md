E-Commerce Sales & Performance Analysis
1. Project Title

E-Commerce Sales & Performance Analysis Dashboard

Project Objective

The objective of this project is to analyze e-commerce sales data to understand sales performance, profitability, customer behavior, product performance, geographical trends, sales channels, payment methods, and order/delivery patterns.

The project uses Python for data cleaning and exploratory data analysis and a dashboard for interactive visualization and business reporting.

2. Problem Statement

E-commerce businesses generate large amounts of transactional and customer data. However, raw data may contain duplicate records, missing values, inconsistent entries, and unstructured date information, making it difficult to directly use for business analysis.

The main problem addressed by this project is:

How can e-commerce transaction data be cleaned, analyzed, and transformed into meaningful business insights that help understand sales, profit, customers, products, regions, channels, and operational performance?

The project therefore focuses on:

Cleaning and preparing raw e-commerce data.
Understanding overall sales and profitability.
Identifying high-performing categories and sub-categories.
Analyzing customer demographics and segments.
Comparing sales across states, cities, and regions.
Evaluating sales channels and payment methods.
Studying monthly, yearly, and daily sales trends.
Presenting the results through an interactive dashboard.
3. Dataset Information

The original dataset contains 10,050 records before duplicate removal and 23 columns. After removing 50 duplicate rows, the working dataset contains 10,000 records.

Dataset size
Information	Details
Original records	10,050
Duplicate records removed	50
Final records	10,000
Original columns	23
Clean dataset columns	29
Customer IDs	4,336
States	9
Categories	7
Sub-categories	35
Sales channels	4
Payment methods	6
Order statuses	4

The original dataset includes customer, order, geographical, product, sales, profitability, payment, rating, and delivery information.

Important columns

Customer information

Customer_ID
Customer_Name
Age
Gender
Customer_Segment

Geographical information

City
State
Region

Product information

Category
Sub_Category
Quantity
Unit_Price

Financial information

Discount_Pct
Sales
Cost
Profit

Operational information

Order_Status
Rating
Delivery_Days

Channel/payment information

Sales_Channel
Payment_Method

The original dataset structure and data types are documented in the EDA work.

4. Data Cleaning Process

Data cleaning was an important part of this project because the raw dataset contained duplicate records, missing values, inconsistent city names, and date fields that required transformation.

Step 1: Identify duplicate records

The dataset initially contained 50 duplicate rows.

df.duplicated().sum()

Result:

50 duplicate records

These duplicate records were removed using:

df = df.drop_duplicates()

After removal:

Duplicate records = 0

Step 2: Check dataset structure

The dataset was examined using:

df.info()

The original dataset contained 23 columns and 10,000 records after duplicate removal.

Step 3: Identify missing values

Missing values were found in:

Column	Missing Values
Age	150
Gender	100
City	119
Discount_Pct	100
Rating	200
Delivery_Days	150
Total	819

The project calculated the overall missing-value percentage as approximately 8.19%.

Step 4: Handle numerical missing values

Missing numerical values were filled using the median.

The numerical columns included:

Age
Quantity
Unit_Price
Discount_Pct
Sales
Cost
Profit
Rating
Delivery_Days

The cleaning code applies median imputation to numerical columns.

This approach is useful because the median is less affected by extreme values than the mean.

Step 5: Handle categorical missing values

Missing categorical values were replaced with "Unknown".

df["Gender"] = df["Gender"].fillna("Unknown")
df["City"] = df["City"].fillna("Unknown")

This prevents the loss of records while clearly identifying originally missing categorical information.

Step 6: Standardize column names

Column names were converted to lowercase:

df.columns = df.columns.str.lower()

For example:

Order_ID → order_id

Customer_Name → customer_name

Payment_Method → payment_method

This makes the dataset easier to work with programmatically.

Step 7: Convert data types

The project converted relevant columns to appropriate data types, including:

age
rating
delivery_days

The date column was also converted into a proper datetime format.

Step 8: Create date-related features

From order_date, the following features were created:

Year
Month
Month Name
Day
Day Name
df["year"] = df["order_date"].dt.year
df["month"] = df["order_date"].dt.month
df["month_name"] = df["order_date"].dt.month_name()
df["day"] = df["order_date"].dt.day
df["day_name"] = df["order_date"].dt.day_name()

These fields enable time-based analysis.

Step 9: Create Age Groups

Customers were divided into five age groups:

Age Group
0–18
19–30
31–45
46–60
60+

This was created using pd.cut().

Step 10: Correct inconsistent city data

The project removed extra spaces and corrected the spelling:

Hyderbad → Hyderabad

df["city"] = df["city"].str.strip()
df["city"] = df["city"].replace('Hyderbad','Hyderabad')

After the cleaning process, the dataset contained no missing values.

5. Overall Business Performance

The cleaned dataset contains:

Total Sales

₹23,200,385

Total Cost

₹15,891,151

Total Profit

₹7,304,314

Total Quantity Sold

19,143 units

The project calculations report these totals directly.

Approximate profit margin

Using:

Profit Margin = Profit / Sales × 100

the overall profit margin is approximately:

31.48%

6. Exploratory Data Analysis
6.1 Gender-wise Sales
Gender	Sales
Male	₹11,544,394
Female	₹11,448,107
Unknown	₹207,884

Male and female customers contribute very similar sales totals.

Insight

Sales are relatively balanced between male and female customers, so the business does not appear to depend heavily on one gender segment.

7. Age Group Analysis
Age Group	Sales
0–18	₹504,996
19–30	₹5,797,105
31–45	₹7,561,496
46–60	₹7,394,615
60+	₹1,942,173

The 31–45 age group generated the highest sales, followed closely by the 46–60 group.

Business Insight

Customers between 31 and 60 years represent a substantial portion of sales, suggesting that this demographic is an important customer group for the business.

8. Customer Segment Analysis
Customer Segment	Sales	Profit
Consumer	₹13,967,728	₹4,398,228
Corporate	₹5,694,282	₹1,795,049
Home Office	₹3,538,375	₹1,111,037

Key Insight

The Consumer segment contributes the largest amount of sales, quantity, and profit in the dataset.

9. State-wise Analysis
State	Sales
Maharashtra	₹4,531,211
West Bengal	₹2,469,961
Telangana	₹2,437,299
Tamil Nadu	₹2,416,423
Karnataka	₹2,368,794
Gujarat	₹2,287,465
Rajasthan	₹2,272,406
Delhi	₹2,265,986
Uttar Pradesh	₹2,150,840

Key Insight

Maharashtra generated substantially more sales than the other states in this dataset and also recorded the highest state-level profit.

10. Region-wise Analysis
Region	Sales	Profit
West	₹5,863,207	₹1,856,010
South	₹5,838,535	₹1,817,105
East	₹5,779,095	₹1,830,010
North	₹5,719,548	₹1,801,189

Key Insight

The four regions have relatively close sales performance, with West showing the highest sales and profit among the four regions in this dataset.

11. Category-wise Analysis
Category	Sales	Profit
Electronics	₹4,662,516	₹1,488,030
Clothing	₹4,314,758	₹1,348,666
Home & Kitchen	₹3,722,840	₹1,169,393
Furniture	₹3,210,863	₹1,024,360
Beauty	₹2,632,962	₹827,567
Books	₹2,350,532	₹729,177
Sports	₹2,305,914	₹717,121

Key Insight

Electronics is the largest category by both sales and profit.

It generated:

₹4.66M sales
₹1.49M profit
3,795 units sold
12. Sub-category Analysis

The major sub-categories by sales include:

Sub-category	Sales
Tablet	₹989,555
Smartwatch	₹989,029
Jeans	₹935,201
Mobile	₹906,472
Laptop	₹905,268
Headphones	₹872,192

By profit, Smartwatch generated the highest profit at approximately ₹325,626, followed by Tablet at approximately ₹317,677.

13. Sales Channel Analysis
Sales Channel	Sales	Profit
Website	₹9,058,403	₹2,858,319
Mobile App	₹7,382,782	₹2,298,241
Marketplace	₹4,630,403	₹1,463,057
Store	₹2,128,797	₹684,697

Key Insight

The Website is the largest sales channel, followed by the Mobile App.

Together, these two digital channels account for a large share of total sales.

14. Payment Method Analysis
Payment Method	Transactions	Sales
UPI	2,979	₹6,947,681
Credit Card	2,226	₹5,118,372
Debit Card	1,587	₹3,768,245
Cash on Delivery	1,533	₹3,345,382
Net Banking	1,141	₹2,708,948
Wallet	534	₹1,311,757

Key Insight

UPI is the most frequently used payment method and also generates the highest sales value.

15. Day-wise Sales Analysis
Day	Sales
Tuesday	₹3,479,872
Sunday	₹3,432,333
Monday	₹3,320,512
Wednesday	₹3,297,162
Friday	₹3,286,740
Thursday	₹3,248,889
Saturday	₹3,134,877

Key Insight

Tuesday has the highest sales in the dataset, while Saturday has the lowest among the seven days.

16. Monthly Sales Analysis

The highest monthly sales were:

Month	Sales
January	₹2,096,357
September	₹2,062,990
November	₹2,013,085
August	₹1,954,482
May	₹1,948,123

The lowest was February at approximately ₹1,809,766.

17. Year-wise Sales
Year	Sales
2024	₹11,479,988
2025	₹11,720,397

Key Insight

Sales increased from 2024 to 2025 by approximately ₹240,409, or about 2.09%.

18. Dashboard

Your dashboard provides an interactive overview of the e-commerce business.

Main dashboard components

KPI Cards

Total Sales
Total Cost
Total Profit
Average Sales per Customer
Average Orders per Day
Total Orders
Sales growth
Total Quantity
Average Sales per Day
Average Order Value
Average Orders per Customer

Filters

Year
State
Category

Visualizations

Sales by Category
Sales by Sales Channel
Sales by Gender
Sales by Year
Sales by Region
Order Status
Rating by Customer
Sales by Age Group
Sales by Day
Sales by Month
Orders & Delivery Days
Payment Method
State/Sub-category details

This dashboard allows management to filter the results by year, state, and category and examine different dimensions of sales performance.

19. Key Business Insights

Based on the complete analysis, the major findings are:

1. Strong overall profitability

The business generated approximately ₹23.2M in sales and ₹7.3M in profit, indicating substantial profitability in the analyzed dataset.

2. Electronics is a major revenue contributor

Electronics generated approximately ₹4.66M sales and ₹1.49M profit, making it the largest category by both measures.

3. Consumer customers dominate

The Consumer segment generated approximately ₹13.97M sales, considerably more than Corporate and Home Office segments.

4. Maharashtra has strong sales performance

Maharashtra generated approximately ₹4.53M sales and ₹1.42M profit.

5. Website is the largest sales channel

Website sales were approximately ₹9.06M, followed by Mobile App sales of approximately ₹7.38M.

6. UPI is the leading payment method

UPI accounted for 2,979 transactions and approximately ₹6.95M sales.

7. Middle-aged customer groups contribute strongly

The 31–45 and 46–60 age groups together contribute a large portion of total sales.

8. Digital channels are important

Website and Mobile App together generate substantially more sales than Marketplace and Store channels.

9. Sales increased in 2025

Sales were approximately ₹11.48M in 2024 and ₹11.72M in 2025.

10. Smartwatch and Tablet are strong sub-categories

Smartwatch and Tablet are the two highest-selling sub-categories by sales, while Smartwatch also records the highest sub-category profit.

20. Business Recommendations

Based on the analysis, the following data-driven actions can be considered:

Focus on high-performing categories such as Electronics and Clothing while monitoring their profitability.
Strengthen website and mobile-app experiences, since these channels account for most sales.
Continue supporting digital payment options, particularly UPI, given its transaction volume.
Develop targeted campaigns for the 31–45 and 46–60 age groups, which contribute strongly to sales.
Analyze Maharashtra separately because of its substantially higher sales and profit contribution.
Monitor lower-performing categories and sub-categories to determine whether pricing, promotion, or product assortment changes are needed.
Use monthly and day-wise trends to plan promotions and inventory.
Track order status and delivery performance to identify operational issues that may affect customer experience.

21. Conclusion

This project demonstrates how raw e-commerce transaction data can be transformed into a structured business intelligence solution through data cleaning, exploratory data analysis, visualization, and dashboard development.

After cleaning the data, the analysis identified important patterns in customer segments, age groups, categories, sub-categories, states, regions, sales channels, payment methods, and time-based sales performance.

The final dashboard provides management with a consolidated view of the company's sales and operational performance and allows users to interactively analyze results using Year, State, and Category filters.

Overall, the project converts raw transactional data into clear, measurable business insights that can support sales planning, customer analysis, product management, and performance monitoring.
