# ### 3.4 Doing More with the INTNX and INTK Functions

The INTNX and INTK functions are used to work with date, time, and datetime intervals. Both can work with a fairly extensive list of interval types; however, you can add even more flexibility to these two functions by using interval multipliers, shift operators, and alignment options.

Using these two functions is not always straightforward; however, you need to be aware of how they make their interval determinations. Of primary importance is that by default they both make their calculations based on the start of the current interval. For instance when using a YEAR interval type for any date in 2009, the current interval will start on January 1, 2009. As a result of

```
```sas
twoday = intck('year','31dec2008'd,'01jan2009'd);
twoyr = intck('year','01jan2008'd,'31dec2009'd);
```
```

the interval start, the two function calls shown here will both return an interval length of one year.

# #### SEE ALSO

Interval multipliers and shift operators are complex topics. Fortunately the documentation for the INTNX and INTK functions is well written and should be consulted for additional important details.

These two functions are carefully described by Cody (2010), and this is a good source for further information on the topics in this section.

# #### 3.4.1 Interval Multipliers

Interval multipliers allow you to alter the definition of the interval length. Interval multipliers are simply implemented as integers that are appended to the standard interval. The interval ‘WEEK’ has a length of 7 days while the same interval with a multiplier of 2 (WEEK2) will have an interval length of 14 days.

In the following rather silly example we would like to schedule a follow-up exam in two weeks (14 days). EXAMDT_2 is calculated to be one two-week interval in the future using an interval multiplier of two ❶.

```
```sas
data ExamSchedule;
   do visdt = '25may2009'd to '14jun2009'd;
      examdt_2 = intnx('week2'❶,visdt,1);
      examdtX2 = intnx('week',visdt,2 ❷);
      output;
   end;
   format visdt examdt_2 examdtx2 date9.;
run;
```
```

EXAMDTX2, on the other hand, is determined by requesting two one-week intervals ❷. Nominally we would expect that the two future dates would be the same; however, because the two INTNX functions measure intervals from the start of their respective interval, the resulting dates are not always the same. The point of this example is to understand why.