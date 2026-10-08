It can be seen in Figure 10 that if two operators with the same priority appear in an expression, they are evaluated based on their associativity, in this case left to right. To modify the sequence of evaluation, we can make use of brackets. If we rewrite the expression as *result = first + second * (third − fourth) / fifth*; then the identifiers third and fourth will be subtracted initially, resulting in intermediate result 1. The intermediate result 1 will then be multiplied with the second, giving intermediate result 2. The intermediate result 2 will then be divided by fifth. Finally, addition with the first will be done. Figure 11 shows the evaluation order of the new expression:

![](bbox=[0.35, 0.26, 0.75, 0.4])

Program 12 illustrates how expressions are evaluated in C:

# ▶ Program 12

```
```c
/* Program to illustrate the evaluation of expression */

#include <stdio.h>
/* Beginning of main function */
main()
{
/* Declaration and initialization of unsigned integer variables */
unsigned int u_first = 25, u_second = 5, u_third = 15;
unsigned int u_fourth = 10, u_fifth = 12, u_result;
/* Expression without brackets */
u_result = u_first * u_second + u_third / u_fourth - u_fifth;
printf("Result of evaluation without using brackets = %d", u_result);
/* Expression with brackets */

u_result = u_first + u_second * (u_third - u_fourth) / u_fifth;
printf("\n Result of evaluation using brackets = %d \n", u_result);
return;
} /* End of function main */
```
```

# Output:

Result of evaluation without using brackets = 114
Result of evaluation using brackets = 27

It can be observed in Program 12 that the output of the same expression drastically changes when brackets are used to control the evaluation. The expressions used in C language are known as C statements. The next section discusses in brief about the statement categories available in C language.