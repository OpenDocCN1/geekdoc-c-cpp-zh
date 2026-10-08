```
title 'Names and Ratings';
proc print data=seminar_ratings;
run;
title;
```

# 4. Reading Multiple Input Records per Observation

```
data sales_staff2;
infile "&path\sales2.dat";ninput @1 Employee_ID 6.
  @21 Last Name $18. /
  @1 Job Title $20.
  @22 Hire Date mmddyy10.
  @33 Salary dollar8.;

run;
```

```
title 'Australian and US Sales Staff';
proc print data=sales_staff2 noobs;
run;
title;
```

# Alternate Solution

```
data sales_staff2;
infile "&path\sales2.dat";
input @1 Employee_ID 6.
  @21 Last Name $18.
input @1 Job Title $20.
  @22 Hire Date mmddyy10.
  @33 Salary dollar8.;n
run;
```

# Alternate Solution

```
data sales_staff2;
infile "&path\sales2.dat";
input @1 Employee_ID 6.
  @21 Last Name $18.
#2 @1 Job Title $20.
  @22 Hire Date mmddyy10.
  @33 Salary dollar8.
#3;

run;
```

# 5. Working with Mixed Record Types

```
data au_sales;
drop Country='sales3.dat';
input @1 Employee_ID 6.
  @21 Last Name $18.
  @43 Job Title $20.;ninput @10 Country $2. @;
if Country = 'AU' then do;
```