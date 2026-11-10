# 6.2. THREE-ADDRESS CODE

+   6. Conditional jumps such as if x relop y goto L, which apply a relational operator (<, ==, >=, etc.) to x and y, and execute the instruction with label L next if x stands in relation relop to y. If not, the three-address instruction following if x relop y goto L is executed next, in sequence.

+   7. Procedure calls and returns are implemented using the following instructions: param x for parameters; call p, n and y = call p, n for procedure and function calls, respectively; and return y, where y, representing a returned value, is optional. Their typical use is as the sequence of three-address instructions

```
```
param x1
param x2
...
param xn
call p, n
```
```

generated as part of a call of the procedure p(x1, x2,..., xn). The integer n, indicating the number of actual parameters in “call p, n,” is not redundant because calls can be nested. That is, some of the first param statements could be parameters of a call that comes after p returns its value; that value becomes another parameter of the later call. The implementation of procedure calls is outlined in Section 6.9.

+   8. Indexed copy instructions of the form x = y[i] and x[i] = y. The instruction x = y[i] sets x to the value in the location i memory units beyond location y. The instruction x[i] = y sets the contents of the location i units beyond x to the value of y.

+   9. Address and pointer assignments of the form x = &y, x = *y, and *x = y. The instruction x = &y sets the r-value of x to be the location (l-value) of y.2 Presumably y is a name, perhaps a temporary, that denotes an expression with an l-value such as A[i][j], and x is a pointer name or temporary. In the instruction x = *y, presumably y is a pointer or a temporary whose r-value is a location. The r-value of x is made equal to the contents of that location. Finally, *x = y sets the r-value of the object pointed to by x to the r-value of y.

**Example 6.5:** Consider the statement

```
```
do i = i+1; while (a[i] < v);
```
```

Two possible translations of this statement are shown in Fig. 6.9. The translation in Fig. 6.9(a) uses a symbolic label L, attached to the first instruction.

2From Section 2.8.3, l- and r-values are appropriate on the left and right sides of assignments, respectively.