## Sales Insights Data Analysis Project

In this project, I have designed a Power BI dashboard to understand the sales trend of ABC Inc's hardware goods. The final dashboard effectively displays the sales trend of ABC Inc's hardware, enabling users to comprehend the data and make informed decisions. This dashboard has the potential to contribute to an increase in revenue of at least 7% in the next quarter.


### Data Analysis Using SQL

1. Show all customer records:

    `SELECT * FROM customers;`

2. Show total number of customers:

    `SELECT count(*) FROM customers;`

3. Show transactions for Chennai market (market code for chennai is Mark001):

    `SELECT * FROM transactions where market_code='Mark001';`

4. Show distrinct product codes that were sold in chennai:

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`

5. Show transactions where currency is US dollars:

    `SELECT * from transactions where currency="USD"`

6. Show transactions in 2020 join by date table:

    `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

7. Show total revenue in year 2020:

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";`
	
8. Show total revenue in year 2020, January Month:

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

9. Show total revenue in year 2020 in Chennai:

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.market_code="Mark001";`


### Data Analysis Using Power BI
============================

1. Formula to create norm_amount column:

`= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)`

2. Formula to create Revenue for last year:

`Revenue LY = CALCULATE([Revenue],SAMEPERIODLASTYEAR('sales date'[date]))`

3. Formula to create Profit Margin %:

`Profit Margin % = DIVIDE([Total Profit Margin],[Revenue],0)`

4. Formula to create Profit margin contribution %:

`Profit margin contribution % = DIVIDE([Total Profit Margin], CALCULATE([Total Profit Margin],ALL('sales products'),ALL('sales markets'), ALL('sales customers')))`

5. Formula to create Revenue contribution %:

`Revenue contribution % = DIVIDE([Revenue], CALCULATE([Revenue],ALL('sales products'),ALL('sales markets'), ALL('sales customers')))`

