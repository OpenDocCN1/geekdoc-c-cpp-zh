9-24 Chapter 9 Combining SAS® Data Sets

| 120400311465 | 13 | Thomas Leitmann |
| 120400312556 | 7 | Robyn Klem |
| 120400315078 | 23 | Tonie Asmussen |
| 120400326278 | 10 | Theunis Brazier |

# # 9.2 Solutions

Solutions to Exercises

+   1. Performing a Match-Merge on Two Data Sets
```sas
data revenue
NotSold(keep=Price Product_ID Product_Name)
InvalidCode(keep=Product_ID Quantity Customer);
merge orion.web_products(in=InProduct)
      orion.web_orders(in=InOrders)
  by Product_ID;
  if InProduct and InOrders then do;
    Revenue=Quantity * Price;
    output revenue;
end;
  else if InProduct and not InOrders then output notold;
  else if not InProduct and InOrders then output invalidcode;
run;
```
```sas
title Revenue from Orders'
proc print data=revenue noobs;
run;
```
```sas
title Products Not Ordered'
proc print data=notsold noobs;
run;
```
```sas
title Invalid Orders'
proc print data=invalidcode noobs;
run;
```

+   2. Handling Same-Named Variables and Different Data Types for BY Variables
```sas
data web_connected(drop=nProduct_ID);
  length Product_ID = $12;
  set orion.web_products2(rename=(Product_ID=nProduct_ID));
  Product_ID=put(nProduct_ID, 12.);
run;
ndata revenue
NotSold(keep=Price Product_ID Product_Name)
InvalidCode(keep=Product_ID Quantity Customer);
merge web_connected(in=InConv rename=(Name=Product_Name))
      orion.web_orders2(in=InOrders rename=(Name=Customer))
  by Product_ID;
```

Copyright © 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.