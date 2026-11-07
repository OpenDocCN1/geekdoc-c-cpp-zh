![](bbox=[0.204, 0.106, 0.889, 0.243])

FIGURE 7-11  Values of the variables when control goes back to Line 6

Line 6 produces the following output:

```
Line 6: After funOne: num1 = 10, num2 = 30, and ch = A
```

The statement in Line 7 is a function call to the function funTwo. Now funTwo has three parameters: x, y, and w. Also, x and w are reference parameters, and y is a value parameter. Thus, x receives the address of its corresponding actual parameter, which is num2, and w receives the address of its corresponding actual parameter, which is ch. The variable y copies the value 25 into its memory cell. Figure 7–12 shows the values before the statement in Line 14 executes.

![](bbox=[0.204, 0.48, 0.889, 0.622])

FIGURE 7-12  Values of the variables before the statement in Line 14 executes

After the statement in Line 14, x++;, executes, the variables are as shown in Figure 7–13. (Note that the variable x changed the value of num2.)

![](bbox=[0.204, 0.738, 0.889, 0.879])

FIGURE 7-13  Values of the variables after the statement in Line 14 executes