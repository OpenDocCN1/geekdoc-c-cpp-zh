array-elements names the elements that make up the array. Array elements can be listed in any order.

+   - Array references cannot be used in compile-time statements such as LABEL, FORMAT, DROP, KEEP, or LENGTH statements.

If you use a function name as the name of the array, SAS treats parenthetical references that involve the name as array references, not function references, for the duration of the DATA step.

+   - The four variables, Qtr1, Qtr2, Qtr3, and Qtr4, can now be referenced via the array name Contrib, with an appropriate subscript.

![](bbox=[0.102, 0.266, 0.671, 0.573])

+   - You can use special SAS name lists to reference variables that were previously defined in the same DATA step. The _CHARACTER_ variable list lists character values only. The _NUMERIC_ variable list lists numeric values.

Avoid using the _ALL_ special SAS name list to reference variables, because the elements in an array must be either character or all numeric values.