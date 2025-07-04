## DSA_Amazon_Product_Review_Analysis
This is my first practice project under the DSA Data Analysis program. Here, I am a Junior Data Analyst at RetailTech Insights, a company that provides e-commerce analytics solutions to sellers on platforms like Amazon.  

My team has been tasked with analyzing product and customer review data to generate insights for Amazon.

My tool for analysis is MS Excel.
### Project Topic
Amazon Product Review Analysis
### Project Overview
As a Junior Data Analyst at RetailTech Insights, a company that provides e-commerce analytics solutions to sellers on platforms like Amazon, my team and I have been 
tasked with analysing product and customer review data to generate insights that can guide product improvement, marketing strategies, and customer engagement. 
### Data Source
A dataset was provided- Amazon case study- for this project [download here](https://docs.google.com/spreadsheets/d/13k0hJFL3V0qJlbYCysdNWIgSPbUWm8Kx/edit?usp=sharing&ouid=111890686017413181401&rtpof=true&sd=true)

The dataset contains information scraped from Amazon product pages, including: 
- Product details: name, category, price, discount, and ratings
- Customer engagement: user reviews, titles, and content

Each row represents a unique product, with aggregated reviewer data stored as comma-separated values 
- Total Records: 1,465 rows
- TotalFields: 16 columns
### Tools Used
- Excel for data collection
- Microsoft word (for documenting steps and findings)
- Microsoft Excel (as the tool for our analysis)
- Microsoft PowerPoint(for presentation of findings)

### Data Cleaning and Preparation
- First, columns not useful for the analysis were eliminated. Such columns include image Link, Product Link, about product, review content 
- Then we removed duplicate produt ids because no two products should have the same id
- Categories were split into multiple levels using the text to columns control in Excel.
- Next, the dataset was checked for errors using the filter command, and the errors corrected. For instance, in the actual price column, an input reads 1,39,900. We will change this to 139,900. Eliminating errors is important as they may affect the result of our analysis.
### Exploratory Data analysis (EDA)
This involves exploring the dataset provided to provide insights. 

***The following are the areas where KMS requires insights to be provided:***
- What is the average discount percentage by product category?
- How many products are listed under each category?
- What is the total number of reviews per category?
- Which products have the highest average ratings?
- What is the average actual price vs the discounted price by category?
- Which products have the highest number of reviews?
- How many products have a discount of 50% or more?
- What is the distribution of product ratings (e.g., how many products are rated 3.0, 4.0, etc.)?
- What is the total potential revenue (actual_price × rating_count) by category?
- What is the number of unique products per price range bucket (e.g., <₹200, ₹200–₹500, >₹500)?
- How does the rating relate to the level of discount?
- How many products have fewer than 1,000 reviews?
- Which categories have products with the highest discounts?
- Identify the top 5 products in terms of rating and number of reviews combined.
  
***Required***
- Use pivot tables and calculated columns
- Using your cleaned dataset and pivot outputs, build an Excel dashboard. 
### Data Analysis and Visualization
This walkthrough will detail the analytical tasks performed on the dataset, which will inform the insights presented to the management at Amazon.
#### ***1. Average discount percentage by product category***
```Excel
Calculated column =(([@[actual_price]]-[@[discounted_price]])/[@[actual_price]])*100 
``` 
Create a pivot table. **Rows**: Category, **Values**: Discount (set to summarize by Average)

#### ***2. Number of products under each category***
Create a pivot table. **Rows**: Category, **Values**: Product name (set to count (distinct))

#### ***3. Total number of reviews per category***
Create a pivot table. **Rows**: category, **values**: Rating Count (sum)

#### ***5.  The average actual price vs the discounted price by category***
Create a pivot table. **Rows**: Category, **Values**: Actual price (set to summarize by Average), Discounted price (set to summarize by Average)

#### ***6. Products with the highest number of reviews***
```Excel
sort Rating Count column in decending order
```

#### ***7. Products with a discount of 50% or more***
```Excel
Calculated column =IF([@[discount_percentage]]>=50%,TRUE,FALSE)
```
And then run the countif like this: 
```Excel
=COUNTIF(calculated column, TRUE) 
```
Our answer is **662**. So there are **662** products with a discount of 50% or more

#### ***8. The distribution of product ratings (e.g., how many products are rated 3.0, 4.0, etc.)?***
Create a pivot table. **Rows**: Ratings, **Values**: product name (count)

#### ***9. Total potential revenue (actual_price × rating_count) by category***
```Excel
Calculated column =[@[actual_price]]*[@[rating_count]]
```
Create a pivot table. **Rows**: Category, **Values**: Total potential revenue (sum)

#### ***10. Number of unique products per price bucket***
```Excel
Calculated column =IF([@[discounted_price]]< 200,"<₹200",IF([@[discounted_price]]<=500,"₹200-₹500",">₹500"))
```
Create a pivot table. **Price range bucket**: Category, **Values**: product name (count)

#### ***12. Products with fewer than 1000 reviews***
Create a pivot table: **Rows**: Category, **Values**: Rating count
Filter rating count < 1000
Use COUNT
There are 15 product categories and 191 products with fewer than 1,000 ratings

#### ***13. Categories with products with the highest discounts***
Create a pivot table: **Rows**: Category, **Values**: Discount percentage (max)

#### ***14. Top 5 products by ratings and number of reviews combined***
```Excel
Calculated column =[@[average_rating]] + ([@[discounted_price]/scaling factor e.g 1000)
```
sort result in descending order

### Summary of Results and Findings

### Recommendations
