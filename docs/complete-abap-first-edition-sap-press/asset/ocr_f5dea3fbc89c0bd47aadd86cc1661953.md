![](bbox=[0.148, 0.103, 0.761, 0.416])

Figure 4.11  Data Type Value List

![](bbox=[0.148, 0.468, 0.547, 0.677])

Figure 4.12  Activating a Data Element

8. If the data type supports decimals, you can also maintain the number of decimal places in the DECIMAL PLACES field.

The data type we just created has global visibility and can be used to define data objects or user-defined data types in any program, as shown:

```
```abap
DATA name TYPE ZCB_PERSON.
TYPES user TYPE ZCB_PERSON.
```
```