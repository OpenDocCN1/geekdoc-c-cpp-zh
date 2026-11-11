![](bbox=[0.034, 0.026, 0.959, 0.657])

You can also use (*) instead of specifying a column name.

```
SELECT COUNT(EMP_NAME)\nFROM SALES_REP;
```

This statement will produce the same result because the EMP_NAME field has no NULL value. Assuming, however, that one of the fields in the EMP_NAME contains a NULL value, this would not be included in the statement that specifies EMP_NAME but will be included in the COUNT() result if you use the * symbol as a parameter.