computation of the function writeVertical is suspended and the following recursive call is executed:

```
writeVertical(12/ 10);
```

which is equivalent to

```
writeVertical(1);
```

At this point there are two suspended computations waiting to resume and the computer begins to execute this new recursive call, which is handled just like all the previous recursive calls. The argument 1 is substituted for the parameter n, and the body of the function is executed. At this point, the computation looks like the following:

![](bbox=[0.2, 0.355, 0.85, 0.625])

Output the digit 1

When the body of the function is executed this time, something different happens. Since 1 is less than 10, the Boolean expression in the if-else statement is true, so the statement before the else is executed. That statement is simply a cout statement that writes the argument 1 to the screen, and so the call writeVertical(1) writes 1 to the screen and ends without any recursive call.

When the call writeVertical(1) ends, the suspended computation that is waiting for it to end resumes where that suspended computation left off, as shown by the following:

![](bbox=[0.22, 0.825, 0.85, 0.965])