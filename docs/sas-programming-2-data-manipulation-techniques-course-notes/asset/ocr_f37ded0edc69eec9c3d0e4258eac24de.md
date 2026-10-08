```
proc sort data=orion.staff out=staff;
  by employee_id;
run;
proc sort data=orion.employee_addresses out=addresses;
  by employee_id;
run;
data sqlEquiv (keep=employee_id job_title salary employee_name);
  merge staff (in=inStaff) addresses (in=inAddr);
  by employee_id;
  if staff and inaddr;
run;
proc print data=sqlEquiv;
run;
```

# 11.04 Short Answer Poll

The orion.customer and orion.country tables both have a column named Country that contains a country abbreviation. Open p211a03 and add a WHERE clause to join the tables based on matching values of Country.

```
sql;
select Customer_ID, Customer_Name,
      Customer.Country, Country_Name
from orion.customer,
      orion.country
where Customer.country = 'Country';
quit;
```

![](bbox=[0.11, 0.545, 0.653, 0.655])