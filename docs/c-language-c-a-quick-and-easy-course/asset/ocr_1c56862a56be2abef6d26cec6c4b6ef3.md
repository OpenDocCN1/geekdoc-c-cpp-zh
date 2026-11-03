possible with the use of the absolute value function. Assume that the program has generated two digits, a and b, through the random function, and you need to know what is the lowest. The mini-program below, which uses stdlib.h and time.h, obtains the two numbers. The use of “time” is so that the random value depends on the moment when the program is executed, otherwise the value of rand() will always be repeated.

```
main() { int a,b; srand(time(NULL)); a=10*rand()/32767;
 b=10*rand()/32767; printf("\n% d %d",a,b);}
```

To decide the minimum value, the formula in regular algebra, is m = (a+b-|a-b|)/2, which translated to C is: m = (a+b-abs(a-b))/2. If we want to get the greatest value, not the lowest, just we exchange for “+” the minus sign that appears before the abs() function.

The exercise for the reader is to build this program, which, recalling, manages two digits a and b through the random function, and then decide which of the two values is the lowest, without using the symbol “<”, printing then this result.