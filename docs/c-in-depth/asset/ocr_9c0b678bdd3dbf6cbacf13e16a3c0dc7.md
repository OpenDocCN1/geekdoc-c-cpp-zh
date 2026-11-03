# Output:

8 42 90

Now the first two printf() give us the desired result. In the third printf we had tried to divide 60 by the product of 2 and 3 and the expected result was 10 but we got 90, so still there is a problem in our macro. Again let us see how preprocessor has done the expansions.

PROD(2, 4) is expanded as (2)*(4)
PROD(3+4, 5+1) is expanded as (3+4)*(5+1)
60/PROD(2, 3) is expanded as 60 / (2)*(3)

Here we can see that in the last case, first 60 is divided by 2 and then the result is multiplied by 3 because / and * operators associate from left to right. So the result was not the expected one. To solve this sort of problem we should enclose whole macro expansion inside parentheses. So the correct way of defining macro is-

```
#define PROD(x, y) ( (x)*(y) )
```

Now 60/PROD(2, 3) would be expanded as 60 / ( (2)*(3) ) and hence 60 is divided by the product of 2 and 3, and we can get the desired result.

So if your macro is accepting arguments and you want it to work properly then it is better to put parentheses around the entire macro expansion and also around each argument.

Now consider this program and we will find another sort of problem.

```
/*P12.6*/
#include<stdio.h>
#define SQUARE(x) ((x)*(x))
main()
{
int k=5,s;
s=SQUARE(k++);
printf("s = %d, k = %d\n",s,k);
}
```

# Output:

s = 25, k = 7

Here the statement
s = SQUARE(k++); is expanded as s = ( (k++) * (k++) );

Here value of k is incremented twice while we intended to assign the square of k to variable s, and then increase the value of k only once. Moreover the result of expressions like (k++)*(k++) is undefined in C. So in this case it is better if we use a function instead of macro.