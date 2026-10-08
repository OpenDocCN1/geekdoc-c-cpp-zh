```
when (5<=ShipDays<=7) output work.slow;
when (ShipDays>7) output work.veryslow;
otherwise;
end;
drop Employee_ID;
```

title 'Orders taking more than 7 days to deliver';
proc print data=work.veryslow;
run;

# 7. Specifying Variables and Observations

```
data work.sales (keep=Employee_ID Job_Title Manager_ID)
work.exec (keep=Employee_ID Job_Title);
set orion_organization;
if Department='Sales' then output work.sales;
else if Department='Executives' then output work.exec;
run;
```

title 'Sales Employees';
proc print data=work.sales (obs=6);
run;

# title;

```
title 'Executives';
proc print data=work.exec (firstobs=2 obs=3);
run;
title;
```

# 8. Specifying Variables and Observations

```
data work.instore (keep=Order_ID Customer_ID Order_Date)
work.delivery (keep=Order_ID Customer_ID Order_Date ShipDays);
set orion.orders (obs=30);
where Order_Type=1;
ShipDays=Delivery_Date-Order_Date;
if ShipDays=0 then output work.instore;
else if ShipDays>0 then output work.delivery;
run;
```

```
data work.instore (keep=Order_ID Customer_ID Order_Date)
work.delivery (keep=Order_ID Customer_ID Order_Date ShipDays);
set orion.orders;
where Order_Type=1;
ShipDays=Delivery_Date-Order_Date;
if ShipDays=0 then output work.instore;
else if ShipDays>0 then output work.delivery;
run;
```

title 'Deliveries from In-store Purchases';
proc print data=work.delivery;
run;