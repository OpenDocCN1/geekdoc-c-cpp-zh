# 7.4.3 Using Percentiles to Create Subsets

The percentile statistics can be used to create search bounds for potential outlier boundaries. Several percentile statistics are available including the 1% and 5% bounds. In this example we would like to know if any observations fall outside of the 1% percentiles.

```
    title1 '7.4.3 Using Percentiles';
    proc summary data=advrpt.lab_chemistry;
        var potassium;
        output out=stats
            p1= ❶
            p99= /autoname;
        run;

    data chkoutlier;
        set stats(keep=potassium_p1 potassium_p99); ❷
        do until (done);
            set advrpt.lab_chemistry ❸
                (keep=subject visit potassium)
                end=done; ❹
            if potassium_p1 ge potassium
                or potassium ge potassium_p99 ❺
                then output chkoutlier;
        end; ❻
    run;
    options nobyline; ❼
    proc print data=chkoutlier;
        by potassium_p1 potassium_p99; ❽
        title2 'Potassium 1% Bounds are #byval1, #byval2'; ❾
    run;
```

+   1. ❶ The 1st and 99th percentiles are calculated and saved in the data set STATS.

+   2. ❷ The single observation of WORK.STATS is added to the Program Data Vector (PDV).

+   3. ❸ The analysis data are read one row at a time in a DO UNTIL loop. The END= option on the SET statement creates the numeric 0/1 variable DONE, which is used to end the loop.

+   4. ❹ Check to see if the current POTASSIUM reading is above or below the 1st and 99th percentiles.

+   5. ❺ A STOP statement has not been used. Although the SET statement is inside the DO UNTIL loop, the STOP is not necessary because all observations have been read from the STATS data set.

+   6. ❻ The NOBYLINE system option removes the BY variable values from the table created by PRINT.

+   7. ❼ A BY statement is used so that the values can be loaded into the #BYVAL options on the TITLE statement.

+   8. ❽ Since the bounds are constants, the #BYVAL option is used to place them in the title. Generally TITLE statements are placed outside of the PROC step; however, for better clarity, when I use the #BYVAR and #BYVAL options I like to move the TITLE statement so that it follows the BY statement.

# MORE INFORMATION

The TITLE statement option #BYVAL is introduced in Section 15.1.2.