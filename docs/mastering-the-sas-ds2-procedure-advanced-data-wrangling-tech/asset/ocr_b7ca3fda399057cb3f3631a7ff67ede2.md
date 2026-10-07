# Mastering the SAS DS2 Procedure: Advanced Data Wrangling Techniques

```
method interest(double Amount, double Rate, int Years)
  returns double;
  decl int i;
  do i=1 to Years
    Amount=SUM(Amount,Amount*Rate);
  end;
  return Amount;
end;
method run();
  set crs.banks;
  do Duration=1 to 5 by 4
    Total=interest(5000,Rate,Duration);
    output;
  end
end;
enddata;
run;
quit;
title:
```

Figure 4.2 shows the results of using the interest method to calculate the final results of depositing $5,000 in each of the banks in the crs.banks data set for a period of one and five years using the modified user-defined interest method. The results are identical to those produced by the previous version. That is to be expected, as we did not change the algorithm used to calculate interest, but only the method used to return the result to the calling process.

Figure 4.2: Results of Using the Modified-Defined Interest Method

Results for each bank - initial $5,000 deposit
method returns a value like a function

| Duration | Bank | Rate |
|---|---|---||
| $5,159.00 | 1 | Carolina Bank and Trust | 0.0318 |
| $5,847.20 | 5 | Carolina Bank and Trust | 0.0318 |
| $5,160.50 | 1 | Big Federal Credit Union | 0.0321 |
| $5,855.70 | 5 | Big Federal Credit Union | 0.0321 |
| $5,164.00 | 1 | National Savings and Trust | 0.0328 |
| $5,875.59 | 5 | National Savings and Trust | 0.0328 |

# 4.2.2.3 The Interest Method – V1.1

Now that everyone in the company is using our new method to do their interest calculations, we detect a flaw: interest can be compounded annually. What if we need to compound the interest quarterly, weekly, or even daily? Let's create version 1.1 of our interest that returns the total after compounding for a user-specified number of periods each year. The new interest calculating algorithm looks like this:

```
do i=1 to Years;
  do j=1 to Periods;
```