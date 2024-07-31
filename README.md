# AtliQ_Products_Analysis
Final project for Tripleten's Data Analyst course. 
The data plots are done with plotly, so the notebook need to be run in order to see them. These are the libraries and versions used for this project:

python 3.10.14
pandas 2.2.1
sqlite 3.41.2
plotly 5.19.0
scipy 1.13.1


The proposed Research Plan is as follows:

# Research Plan: Data Analysis of Product Data

## Introduction
Our team has been commissioned by AtliQ Hardware to conduct a thorough analysis of their product portfolio and sales data.<br> As a prominent computer hardware producer in India, AtliQ is keen on enhancing their understanding of product performance. This analysis aims to identify top-selling products, uncover trends, and develop strategies to optimize sales and market share.

## Objective
The primary objective of this research is to analyze AtliQ Hardware's product portfolio and sales data to better understand product performance and identify strategies for optimizing sales. We aim to answer key questions such as:
- Which products are the top sellers within AtliQ's portfolio?
- How have market preferences for these products evolved over time and across different regions?

Through this analysis, our goal is to provide AtliQ Hardware with actionable insights and recommendations to help drive business growth.

## Data Description
The dataset provided by AtliQ Hardware comprises information on their product portfolio, sales transactions, and customer demographics. The main entities in the dataset for our analysis include:

- **Products**: Information on the various hardware products offered by AtliQ, including product IDs, names, categories, and pricing details.
- **Sales Transactions**: Data on sales transactions, including customer IDs, product IDs, and quantities. The sales data is aggregated by month and customer.
- **Customers**: Demographic information about customers, such as country, region, and type (e.g., distributors, retailers, direct customers).

The available data is from `Sept 2017` to `Dec 2021`. This encompasses fiscal years 2018 to 2022.

Additionally, the dataset includes fields detailing product variants, such as color variations, and manufacturing cost per year for each product. 

While we won't delve into the specific database schema in this document, the provided dataset encompasses the necessary information for conducting in-depth analysis of product performance and sales trends.


## Research Questions

- Which items are the bestsellers?
- How has popularity changed over time/across markets?We can then split that data using `fact_sales_monthly.fiscal_year` to get the yearly totals, or by `date` if we want to reveal any seasonality.
- Are there some variants that contribute a disproportionate amount to the product sales?
- Is the demand of some of our products coming largely from a specific channel?
- What are the products with the best/worst margin?
- Is gross price keeping up with manufacturing costs?


## Methodology
- **Finding bestsellers**: The table `fact_sales_monthly` has the sales data by `product_code`. 
- **Popularity across time and markets**: We can modify the previous step to divide the sales according to `fact_sales_monthly.fiscal_year` to get yearly data; or we can group the sales according to 'fact_sales_monthly.date' to see sales per month, which can reveal seasonalities in some products. We can link 'fact_sales_monthly' and 'dim_customer' though `customer_code`, and that would let us group the data by `dim_customer.market` to get the sales in each market.
- **Variant sales**: By comparing the total sale of each `fact_sales_monthly.product_code` to the total sales of their product, we can find variants whose contribution to the total is too low or too high.
- **Division sales**: Similar to variant sales, we can get the total sales per `dim_product.division` and then check the contibution of each `dim_customer.channel` to it, looking for channels whose contribution is much greater than the norm.
- **Product margin**: We can sustract `fact_manufacturing_cost.manufacturing_cost` from  `fact_gross_price.gross_price`, linking them through `product_code` and `fiscal_year/cost_year`.
- **Price vs cost**: A negative margin value would indicate that the product is generating loses. Since we have yearly data, we can see how this value progresses in time.

