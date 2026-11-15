We can also assign a value from one variable to another with an assignment statement:

```
rate = state_tax;
```

The equal sign should be read as “is assigned the value of”; thus, this statement is “rate is assigned the value of state_tax.” If state_tax contains the value 0.06, then rate also contains the value 0.06 after the statement is executed; the value in state_tax is not changed. Thus, the memory snapshots before and after this statement is executed are the following:

| | rate | state_tax |
| :--- | :--- | :--- |
| Before: | 7 | 0.06 |
| After: | 0.06 | 0.06 |

If we assign a value to a variable that has a different data type, then a conversion must occur during the execution of the statement. Sometimes the conversion can result in information being lost. For example, consider the following declaration and assignment statement:

```
int a;
...
a = 12.8;
```

Because a is defined as an integer, it cannot store a value with a nonzero decimal portion. Therefore, in this case, the memory snapshot after executing the assignment statement is the following:

| a | 12 |
|---|---|

To determine whether a numeric conversion will work properly or not, we use the following order (from high to low):

+   high: long double
+   double
+   float
+   long integer
+   integer
+   low: short integer

If a value is moved to a data type that is higher in order, no information will be lost; if a value is moved to a data type that is lower in order, information may be lost. Thus, moving an integer to a double will work properly, but moving a float to an integer may result in the loss of some information or in an incorrect result. In general, use only assignments that do not cause potential conversion problems. (Unsigned integers were not included in the list because errors can occur in both directions.)

# Arithmetic Operators

An assignment statement can be used to assign the result of an arithmetic operation to a variable, as shown in this statement that computes the area of a square:

```
area_square = side*side;
```