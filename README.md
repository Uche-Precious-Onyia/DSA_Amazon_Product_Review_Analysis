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
Calculated column =((actual price-discounted price)/actual price)*100 
``` 
Create a pivot table. **Rows**: Category, **Values**: Discount (set to summarize by Average)
#### ***2. Number of products under each category***
Create a pivot table. **Rows**: Category, **Values**: Product name (set to count (distinct))

#### ***3. Total number of reviews per category***
Create a pivot table. **Rows**: category, **values**: Rating Count (sum)

#### ***4. Products with the highest average ratings***

#### ***5.  The average actual price vs the discounted price by category***
Create a pivot table. **Rows**: Category, **Values**: Actual price (set to summarize by Average), Discounted price (set to summarize by Average)

#### ***6. Products with the highest number of reviews***
```Excel
sort Rating Count column in decending order
```

#### ***7. Products with a discount of 50% or more***
```Excel
Calculated column =IF(Discount percentage>=50%,TRUE,FALSE)
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
=Calculated column =Actual price*Rating count
```
Create a pivot table. **Rows**: Category, **Values**: Total potential revenue (sum)

#### ***10.   Most profitable consumer customer***

#### ***11. Customers with returned items and their segments***

#### ***11. Shipping costs based on the Order Priority***
```SQL
select  ship_mode, order_priority, sum (shipping_cost) as [Total shipping cost]
from (select ship_mode, order_priority, shipping_cost from [Order ]) as [Most Profitable Consumer Customer] 
where Ship_Mode = 'delivery truck' or Ship_Mode = 'Express air'
group by ship_mode, Order_Priority
order by [Total shipping cost] desc
```
If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, did the company appropriately spend shipping costs based on the Order Priority? To determine when a company appropriately spends shipping costs based on order priority, we can categorize the shipping methods according to the urgency of the orders. 

***Shipping Methods***
- Delivery Truck
  - Cost: Most economical
  - Speed: Slowest
- Express Air
  - Cost: Most expensive
  - Speed: Fastest

***Order Priorities***
- Critical: Requires immediate delivery.
- High: Needs prompt delivery but not as urgent as critical.
- Medium: Standard delivery timeframe is acceptable.
- Low: Can wait for delivery without any rush.

***Appropriate Shipping Costs Based on Order Priority***
  
| Order Priority | Recommended Shipping Method |  Justification |
| ------------- | ------------- | ------------- |
| Critical	Express  | Air | Immediate delivery is essential to meet urgent needs |
| High  | Express Air or Delivery Truck	Depending on the specific urgency and availability of budget  | Express Air if budget allows; otherwise, Delivery Truck if acceptable |
| Medium  | Delivery Truck  | Cost-effective option is suitable for standard delivery times |
| Low  | Delivery Truck  | Most economical choice is appropriate for non-urgent deliveries |

A look at the results generated below shows that the company is incurring higher shipping costs for delivery trucks over Express Air across all order priorities. This indicates a misalignment with the principles of cost-effectiveness, order priority, and customer satisfaction. Therefore, we cannot say that the comapany appropriately spent shipping costs based on the Order Priority.

![image](https://github.com/user-attachments/assets/a83cc32a-c4be-485f-84e9-8d4f81e4f67e)
### Summary of Results and Findings
- The product category with the highest sales is Technology with 5984248.409
- The top 3 regions in terms of sales are the **West** with **3597549.329**, **Ontario** with **3063212.527** and **Prarie** with **2837304.650** and the bottom 3 regions in terms of sales are **Nunavut** with **116376.486**, **Northwest Territories** with **800847.341**, and **Yukon** with **975867.383**
- KMS incurred the most shipping cost of **51971.940** using **Delivery Trucks**
- The small business customer with the highest sales is **Dennis Kane** with **75967.591**
- **Roy Skaria** ranks the highest from KMS' corporate customers with **773** orders placed between 2009 and 2012
- The most profitable consumer customer is **Emily Phan** with profit of **34005.440**
  
### Recommendations
- Product Category for focus: since technological products have brought the most revenue for KMS in the last three years, then the company is advised to really rein in on improving its production and sale of those products across its different markets.
- Regional Sales: The top 3 regions in terms of sales are the **West** with **3597549.329**, **Ontario** with **3063212.527** and **Prarie** with **2837304.650** and the bottom 3 regions in terms of sales are **Nunavut** with **116376.486**, **Northwest Territories** with **800847.341**, and **Yukon** with **975867.383**. The company is advised to channel most of its focus to making available its products in its biggest markets; the West, Ontario, and Prarie.
- The most valuable customers typically purchase technological products. And since our analysis has already revealed that technological products have brought KMS the most benefit, then this is another pointer to the fact that the company needs to prioritize the production and sale of its technological products across its different markets.
- Loyalty programs can be implemented for the business' most valuable and profitable customers. Customers may perceive greater value in their purchases when they know they are earning rewards, leading to increased spending. Loyalty programs foster a sense of connection between customers and brands, leading to increased trust and satisfaction. Customers who feel rewarded and recognized are more likely to develop a preference for a brand over competitors, leading to higher retention rates.
- From our results, furniture and office supplies have not sold well mainly to consumers, home offices, and small businesses. Customers in these segments also represent KMS' bottom customers in terms of sales. The company may implement some or all of these strategies:
  - Conduct Surveys: Gather feedback from these customers to understand their specific needs, preferences, and pain points regarding furniture and office supplies.
  - Tailored Promotions: Create personalized offers based on their purchase history or preferences. For example, if a customer frequently buys ergonomic chairs, offer discounts on related products.
  - Create Bundles and seasonal promotions: Offer bundles that combine complementary products (e.g., a desk with an office chair and supplies) at a discounted rate to encourage larger purchases. Introduce seasonal bundles that cater to specific needs, such as back-to-school or home office setups.
  - Enhanced Customer Support: Offer dedicated support for these segments, ensuring they receive quick responses to inquiries and assistance with product selection.
  - Leverage social proof using Customer Reviews and Testimonials and case studies: Highlight positive reviews and testimonials from similar customers to build trust and encourage purchases. Share success stories of how other small businesses or home offices have benefited from your products.
- Shipping Costs:
  - Cost-Effectiveness: Delivery Truck is typically the most economical option. If the company is paying more for delivery trucks than for Express Air, it indicates a misallocation of resources. The expectation is that the least expensive option should be used for lower-priority orders.
  - Order Priority Alignment: Critical and High Priority Orders should prioritize speed over cost. If the company is using delivery trucks (which are slower) and incurring higher costs, it contradicts the need for timely delivery for these orders. This suggests a failure to align shipping methods with the urgency of the orders.
  - Inefficient Resource Management: Spending more on a slower shipping method indicates poor decision-making. The company should assess shipping needs based on urgency and choose the method that balances cost with delivery speed. Higher costs for delivery trucks suggest inefficiency.
  - Customer Satisfaction: If critical orders are delayed due to the use of delivery trucks, it can lead to customer dissatisfaction. Meeting customer expectations is crucial, especially for critical and high-priority orders, which require timely fulfillment.
  - Financial Implications: Higher shipping costs for delivery trucks could negatively impact the company's profitability. It is essential to optimize shipping strategies to maintain a healthy bottom line while meeting customer demands.
