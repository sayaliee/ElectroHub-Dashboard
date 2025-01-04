# ElectroHub Dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/279f382f-3947-4aad-bafd-ffd051a8d1eb/e69ec558020b3c00d882?experience=power-biSection

## Problem Statement

This dashboard helps the ElectroHub to understand their products and customers better. It helps the ElectroHub company know their products and sales throughout various parts of India. Through different sales data, they get to know their improvement area, & thus they can improve their products and strategies by identifying these area. It also lets them know the trends based on the timeline and so they can know which type of products are booming aroung what time.

It helps ElectroHub to monitor the total profit, total sales and total orders according to various factors affecting. 


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present except the Sheet3 was to be named as fact table.
- Step 5 : Data Modelling was done by using cardinality on these tables to form a Star Schema.
- Step 6 : In the fact table, new columns like 'Price Per Unit','Total Sales', 'Discount Percentage', 'Net Sales' , 'Discount Value' were added.
- Step 7 : To calculate 'Price Per Unit', left outer join was performed on the fact table and Dim Product using 'Product ID', and 'Price' column was expanded.
- Step 8 : To calculate 'Total Sales', 'Units Sold' and 'Price Per Unit' were multiplied.

        Total Sales = 'Fact Table'[Units Sold] * 'Fact Table'[Price Per Unit']
- Step 9 : To calculate 'Discount Prcentage', left outer join was performed on the fact table and Dim Promotion using 'PromotionID', and 'Percentage' column was expanded.
- Step 10 : To calculate 'Discount Value', custom column was made using the given formula

        Discount Value = 'Fact Table'[(Total Sales] * 'Fact Table'[Discount Percentage])/100
- Step 11 : To calculate 'Net Sales', custom column was made using the given formula

        Net Sales = 'Fact Table'[Total Sales] - 'Fact Table'[Discount Value]
- Step 12 : To calculate 'Profit', we took 10% of the 'Net Sales' as Profit

        Profit = 'Fact Table'[Net Sales] * 0.1
- Step 13 : Following New Measures were created using DAX queries given below

        Total Profit = SUM('Fact Table'[Profit])

        Total Orders = COUNT('Fact Table'[Order ID])

        Total Net Sales = SUM('Fact Table'[Net Sales])
