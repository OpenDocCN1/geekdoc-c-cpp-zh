# Logical NOT (!)

The operator converts a true value into false and vice-versa. Again the operand may be any expression, constant, variable or function.

```
/*PROG 3.10 DEMO OF LOGICAL OPERATOR !(NOT) VER 1 */

#include <iostream.h>
void main()
{
int res, a=1;
    res = !a;
cout<< "Returned value in res= " <<res<<endl;
}

OUTPUT :
Returned value in res= 0
```

![](bbox=[0.275, 0.432, 0.73, 0.508])

Figure 3.10. Output screen of program.

EXPLANATION : The! is called NOT or negation operator. It is an unary operator meaning only one operand is required on it. If operand's value is non-zero it is converted into false value that is 0 and vice-versa. Similarly if a true condition is specified it will be turned into false and vice-versa. Try changing value of a to zero, returned value in res will be 1.

```
/*PROG 3.11 DEMO OF LOGICAL OPERATOR (NOT ! OPERATOR) VER 2 */

#include <iostream.h>
void main()
{
    int res;
res = !(10>5 && -4 <= 1);
cout<< "returned value in res  := " << res <<endl;
}

OUTPUT :
returned value in res  := 0
```