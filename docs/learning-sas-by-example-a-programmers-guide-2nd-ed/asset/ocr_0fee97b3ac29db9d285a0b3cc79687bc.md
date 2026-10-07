Here is the output:

# Figure 17.9: Output from Program 17.8

| Color | Frequency |
|---|---|
| Yellow | 2 |
| Blue | 3 |
| Red | 4 |
| Green | 1 |

Notice that the values are ordered by the internal values of ORDER= Color.

The next program demonstrates how the other ORDER= options work:

# Program 17.9: Demonstrating the ORDER= Formatted, Data, and Freq Options

```
title "ORDER = Formatted";
proc freq data=Test order=formatted;
tables Color / nocum nopercentent;
format Color Colors;
run;

title "ORDER = Data";
proc freq data=Test order=data;
tables Color / nocum nopercentent;
format Color Colors;
run;

title "ORDER = Freq";
proc freq data=test order=freq;
tables Color / nocum nopercentent;
format Color Colors;
run;
```