```
int original, rem, result =0, n =0, flag;
original=num;
while(original !=0){
original%=10;
+in;
}
original=num;
while(original !=0){
rem= original%10;
result+=pow(rem, n);
original/=10;
}
// condition for Armstrong number
if(result==num)
flag=1;
else
flag=0;
return flag;
}
```

# Output

Enter a positive integer: 407
407 is not a prime number.
407 is an Armstrong number.

# 29. Write a C program to calculate the power using recursion.

```
#include<stdio.h>
int power(int n1
```