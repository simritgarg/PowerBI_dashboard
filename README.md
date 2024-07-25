# Sales Insights - Dashboard

### Dashboard Link : (https://github.com/user-attachments/assets/c97bd9f5-ef6d-4191-ad43-4f78bb478aa2)


## Problem Statement

There was a case study of a company who was facing decline in their sales so this dashboard helps the company understand their sales better. It helps the company  to know how their sales were in last few years so that they can improve their declining sales. Through different factors, they get to know their improvement area, & thus they can improve their sales by identifying these area. It also lets them know the loses, thus since by using this dashboard they have identified this problem, they can further work on factors responsible for these declining sales.

In the dataset, I was having these following data.
The Folder name is sales, In these folder, I have 5 different folders
1. markets:
having columns:-  market_code, market_name, zone;
2. Date: 
having columns:-  date, year, month, cy_date, mm_date;
3. customers:
having columns:-  custmer_code, customer_name, customer_type;
4. Product:
having columns:-  product_code, product_type;
5. Transactions:
having columns:-  market_code, customer_code, product_code, order_date, sales_qty, sales_amount, currency;

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in some of the columns there was missing values in "sales markets" column and different units in "sales transactions" column.
- Step 5 : In "sales markets", null values were not taken into account as only 2 rows were there who have unknown "zone" and there were some rows for which "sales_amount" was in "USD" and others were in "INR". 


### Data Analysis Using SQL

1. Show all customer records

    `SELECT * FROM customers;`

2. Show total number of customers

    `SELECT count(*) FROM customers;`

3. Show transactions for Chennai market (market code for chennai is Mark001

    `SELECT * FROM transactions where market_code='Mark001';`

4. Show distrinct product codes that were sold in chennai

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`

5. Show transactions where currency is US dollars

    `SELECT * from transactions where currency="USD"`

6. Show transactions in 2020 join by date table

    `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

7. Show total revenue in year 2020,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";`
	
8. Show total revenue in year 2020, January Month,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

9. Show total revenue in year 2020 in Chennai

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
and transactions.market_code="Mark001";`


Data Analysis Using Power BI
============================
"norm_sales_amount" column was created to convert all "sales_amount" "USD" currency in "INR" currency only.
1. Formula to create norm_sales_amount column

`= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)`

