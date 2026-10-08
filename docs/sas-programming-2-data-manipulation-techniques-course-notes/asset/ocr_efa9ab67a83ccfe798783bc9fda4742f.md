# 9.1 Using Data Manipulation Techniques with Match-Merging

# # Create Gift List: Solution

Use the IN= option and a condition in the subsetting
IF statement to keep only the matches.

```
libname bonus "&path;BonusGift.xls";

data CustorProdGift;
  merge CustorProd$'n(in=s)
    rename=(SuppID=Supplier
           Quantity=Minimum));
by Supplier;
  if c=1 and s=1 and Quantity > Minimum;
run;

libname bonus clear;
```

![](bbox=[0.045, 0.388, 0.615, 0.403])

# # Create Gift List: Solution

Fifty-two gifts are sent to customers.

# Partial SAS Log

```
207 libname bonus "&path;BonusGift.xls"
NOTE: LIBNAME BONUS was successfully assigned as:
      DATA
      Physical Name: BonusGift.xls
208 data CustorProdGift;
209 merge CustorProd(in=s)
210   Bonus.Supplier$n(in=s)
211   rename=(SuppID=Supplier
            Quantity=Minimum));
212 by Supplier;
213   if c=1 and s=1 and Quantity > Minimum;
214 run;
```

NOTE: There were 148 observations read from the data set WORK.CUSTOPD.
NOTE: There were 18 observations read from the data set BONUS$'n.
NOTE: The DATA statement created 148 observations and 7 variables.
NOTE: DATA statement used (Total process time):
real time    0.03 seconds
cpu time      0.03 seconds