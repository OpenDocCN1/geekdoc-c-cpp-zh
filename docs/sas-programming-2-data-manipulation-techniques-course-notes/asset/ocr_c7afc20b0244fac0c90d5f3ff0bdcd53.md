# 7.02 Short Answer Poll

How can you generate a separate observation for each year?

```
data invest;
do Year=2008 to 2010;
  Capital=5000;
  Capital+(Capital*.045);
end;
output;
run;
proc print data=invest noobs;
run;
```

# Exercises

If you restarted your SAS session since the last exercise, open and submit the libname.sas program found in the data folder.

# Level 1

1. Performing Computations with DO Loops

The Orion Star Payroll Department must project total employee costs (wages, retirement benefits, and medical benefits) through future years, based on assumed increases.

a. Open the file p207e01 and make the following changes:

+   - Insert a DO loop containing statements to calculate the estimated values of Wages, Retire, and Medical.
- Use Start and Stop to control the values of the index variable, Year.
- Assume the estimated annual increase shown in the table below. For example, to calculate Wages, using this formula:
  wages = wages * 1.06;

| Variable | Current Value | Estimated Annual Increase |
| Wages | $12,874,000 | 6.0% |
| Retire | 1,765,000 | 1.4% |
| Medical | 649 | 9.5% |