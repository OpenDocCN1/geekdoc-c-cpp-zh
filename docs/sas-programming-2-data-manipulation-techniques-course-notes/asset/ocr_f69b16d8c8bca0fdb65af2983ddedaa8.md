11-20 Chapter 11 Other SAS Languages

# Partial PROC SQL Output

| Product Name | Supplier Start Date |
| Osprey Girl's Tights | US | 01DEC2011 |
| Big Guy Men's Woven Warm Up | US | 01JUL2011 |
| Woman's Foxhole Jacket | US | 01JUL2011 |
| Armadillo Road Dmx Men's Running Shoes | CA | 01JUN2011 |
| ... | | |
| Amber Cc | CA | 01DEC2011 |

b. Modify this program as follows:

+   - Display the columns Product_ID, Product_Name, Start_Date, End_Date, and Discount as shown below.
- Modify the WHERE clause so that only rows with Discount greater than or equal to .60 are returned. Discount is stored as a proportion but displayed as a percentage using the PERCENT. Format.

Hint: Add an AND to the WHERE clause to put in the condition for Discount. Also, remember to qualify any columns that appear in both tables.

# Partial PROC SQL Output

| Product ID Product Name | Start Date End Date Discount Price |
| 22010100309 Big Guy Men's Woven Warm Up | 01JUL2011 31JUL2011 60% |
| 22010100536 Woman's Foxhole Jacket | 01JUL2011 31JUL2011 60% |
| 22010070023 Armadillo Road Dmx Men's Running Shoes | 01JUN2011 30JUN2011 70% |
| 22010070024 Armadillo Road Dmx Women's Running Shoes | 01JUL2011 31JUL2011 60% |
| 24070400002 Stephens Shirt | 01JUN2011 30JUN2011 70%

# Level 2

# 2. Coding a PROC SQL Inner Join

+   - The table order_order_fact contains a group of orders.
- The table order.product_dim contains descriptions of products.
- Both tables have a column named Product_ID.

Partial order_order_fact (617 Total Rows, 12 Total Columns)

| Product_ID Order_ID | Quantity |
| 22010300017 | 1230058123 | 1 |
| 23010500026 | 1230080101 | 1 |
| 24060100080 | 1230106883 | 1 |
| 24060100010 | 1230147441 | 2 |

Copyright © 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.