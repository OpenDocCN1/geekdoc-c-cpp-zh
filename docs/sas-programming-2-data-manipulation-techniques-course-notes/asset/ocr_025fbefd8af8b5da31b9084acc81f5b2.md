# 9.03 Short Answer Poll

What two temporary variables are created due to the BY statement?

```
data orders (keep=Customer Name Quantity
Product ID Total Retail_Price)
noorders (keep=Customer Name Birth Date);
merge orion.customer
work.order_fact(in=order);
by Customer ID;
if order=1 then output orders;
else output noorders;
run;
```

![](bbox=[0.235, 0.313, 0.563, 0.386])

# First, and Last. Variables and Sum Statement

The First. and Last. variables along with the sum statement can be used to create the values for the summary data set. 

```
data orders (keep=Customer Name Quantity
Product ID Total Retail_Price)
noorders (keep=Customer Name Birth Date)
summary (keep=Customer Name NumOrders);
merge orion.customer
work.order_fact(in=order);
by Customer ID;
if order=1 then do;
output orders;
if first.Customer ID then NumOrders=0;
NumOrders+1;
if last.Customer ID then output summary;
end;
else output noorders;
run;
```