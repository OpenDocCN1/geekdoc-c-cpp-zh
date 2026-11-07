![](bbox=[0.182, 0.107, 0.912, 0.275])

**FIGURE 7-8** Values of the variables after the statement in Line 10 executes

After the statement in Line 11, `b = b * 2;` executes, the variables are as shown in Figure 7-9. (Note that the variable `b` changed the value of `num2`.)

![](bbox=[0.182, 0.374, 0.912, 0.547])

**FIGURE 7-9** Values of the variables after the statement in Line 11 executes

After the statement in Line 12, `v = 'B';` executes, the variables are as shown in Figure 7-10.

![](bbox=[0.182, 0.627, 0.912, 0.796])

**FIGURE 7-10** Values of the variables after the statement in Line 12 executes

The statement in Line 13 produces the following output:

```
Line 13: Inside funOne: a = 11, b = 30, v = B, and one = 10
```

After the statement in Line 13 executes, control goes back to Line 6 and the memory allocated for the variables of function funOne is deallocated. Figure 7-11 shows the values of the variables of the function main.