# Part IV: Analyzing Data in Microsoft Access

[Revenue]-NZ([Yesterday],0), as shown in Figure 15.23. Note that the Yesterday field is wrapped in an NZ function in order to avoid errors caused by null fields.

# FIGURE 15.23

Enhance your analysis by adding a variance between today and yesterday.

![](bbox=[0.18, 0.35, 0.92, 0.53])

Figure 15.24 shows the result.

# FIGURE 15.24

Another task made possible by domain aggregate functions.

| OrderDate | Revenue | Today vs Yesterday | Yesterday |
|---|---|---|---|
| 1/5/2008 | $1,218.87 | $1,218.87 | |
| 1/6/2008 | $29,280.65 | $28,061.78 | 1218.8734 |
| 1/7/2008 | $34,418.48 | $5,137.83 | 29280.6534 |
| 1/8/2008 | $34,437.67 | $19.19 | 34418.4828 |
| 1/9/2008 | $41,319.75 | $6,882.07 | 34437.6745 |
| 1/12/2008 | $37,923.82 | ($37,923.82) | |
| 1/13/2008 | $37,900.75 | ($23.07) | 37923.8214 |
| 1/14/2008 | $33,318.55 | ($4,582.20) | 37900.7498 |
| 1/15/2008 | $44,478.61 | $11,160.06 | 33318.5515 |
| 1/16/2008 | $31,350.05 | ($13,128.57) | 44478.8144 |