# NOTE

Keep in mind that the value returned when passing a date through a Format function is a string that cannot be used in subsequent calculations.

The query in Figure 12.29 shows how you would group all the order dates into quarters and then group the quarters to get a sum of revenue for each quarter.

# FIGURE 12.29

You can group dates into quarters by using the Format function.

![](bbox=[0.22, 0.45, 0.66, 0.68])

If you want to get fancy, you can insert the Format function in a crosstab query, using Quarter as the column (see Figure 12.30).

As you can see in Figure 12.31, the resulting data set is a clean look at revenue by product by quarter.

# The DateSerial function

The DateSerial function allows you to construct a date value by combining given year, month, and day components. This function is perfect for converting disparate strings that, together, represent a date, into an actual date:

```
DateSerial(Year, Month, Day)
```

The DateSerial function has three arguments:

+   - Year (required): Any number or numeric expression from 100 to 9999
+   - Month (required): Any number or numeric expression
+   - Day (required): Any number or numeric expression