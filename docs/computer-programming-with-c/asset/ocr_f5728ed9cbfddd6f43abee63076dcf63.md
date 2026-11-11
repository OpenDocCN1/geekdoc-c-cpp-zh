![](bbox=[0.273, 0.108, 0.716, 0.362])

# ### 2.5.4 _unsigned_ keyword

The range of the values that a variable stores can be extended if the variable is required to store only the positive values instead of storing positive as well as negative values. For example, the range of integer variable can be increased from 0 to 65535 instead of −32768 to +32767, if we support storage of positive numbers only. C/C++ supports a keyword unsigned which informs the compiler that the programmer will not be storing any negative numbers in the variable. For example, the below statement creates an unsigned integer type of variable which is named as marks.

```
```c
unsigned int marks;
```
```

This informs the compiler that the value of variable marks can never be negative. The keyword unsigned can be similarly applied to other data types as well.

# ### 2.5.5 Rules for naming variables

A variable name is a sequence of letters and digits. Given below are a set of rules that the programmer must follow while naming variables:

+   1. Variable name cannot contain special characters such as comma, semicolon, and space, however, we can have an underscore (symbol _) as a part of the variable name.
+   2. The variable name cannot begin with a number. This means that the first symbol of the variable name can be a letter or an underscore.
+   3. A variable name cannot be same as that of a built-in keyword of C/C++. Appendix II gives the list of keywords supported by C and C++.

Given below are the examples of valid and invalid variable names of variables

| Variable name | Remark |
|---|---|
| `roll_no` | This is a VALID variable name. |
| `Sum` | This is a VALID variable name. |