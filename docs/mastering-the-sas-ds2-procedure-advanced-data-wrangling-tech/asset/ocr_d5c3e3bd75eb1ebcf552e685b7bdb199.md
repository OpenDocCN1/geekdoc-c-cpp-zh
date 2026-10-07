# 5.2.2.2 Using FCMP Functions in DS2

First, we will need to create a DS2 wrapper package for the SAS data set containing the FCMP functions. The following DS2 program creates that wrapper package:

```
/*/Wrapper the PROC FCMP functions in a DS2 package*/
proc ds2;
    package crs.DS2_fcmp_funcs / overwrite=yes language='fcmp'
    table='crs.fcmp_functions';

run;
quit;
```

Now we can use an instance of a wrapper package just like any other package in DS2. The FCMP functions are called like DS2 methods:

```
/*Use the DS2 package of PROC FCMP functions*/
proc ds2;
    data work.underperforming_ds2 (overwrite=yes);
        dcl package crs.ds2_fcmp_funcs my myPkg();
        dcl double Product having format 12. label 'Product ID';
        dcl double GrossSales having format dollar1.2
            label 'Gross Sales';
        dcl double CostOfGoods having format dollar1.2
            label 'Cost of Goods';
        dcl double GrossMargin having format percent7.1
            label 'Gross Margin %';
        dcl double Fixed having format dollar1.2 label 'Fixed Costs';
        dcl double Units having label 'Units Sold';
        dcl double BreakEven having label 'Break Even (Units)';
        dcl double GrossProfit having format dollar1.2
            label 'Gross Profit (Total)';
        dcl double NetRevenue having format dollar1.2
            label 'Net Revenue';
        method run();
            set crs.DS2_2014;
            /*/This code uses the ourBE method from myPkg*/
            BreakEven=myPkg.ourBE(GrossSales,CostOfGoods,Fixed,Units);
            if breven > 0
            then begin
                /*/This code uses the custom ourGMP function *//
                GrossMargin=myPkg.ourGMP(GrossSales,CostOfGoods);
                NetRevenue=GrossSales-CostOfGoods-Fixed;
            end;
        end;
run;
quit;

    title "Underperforming Sales Items - DS2 Data Step";
    proc print data=work.underperforming_ds2 noobs label;
        var SupplierName ProductName Product_ID UNITS;
        var BreakEven;
        var GrossSales CostOfGoods Fixed GrossMargin NetRevenue;
    run;
    title;
```