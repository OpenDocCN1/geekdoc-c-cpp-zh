```
cout << "Returned value in res= " << res << endl;
}
```

# OUTPUT :

Returned value in res= 0

![](bbox=[0.28, 0.23, 0.72, 0.31])

Figure 3.8. Output screen of program.

EXPLANATION : In the expression the condition before && is false and after && it is true so overall value of the expression is false so a 0 is assigned to res.

# Logical OR (||)

The operator works with two operands which may be any expression, variable, constant or function. It checks any of its operand returns true value or not. If they it returns true value i.e., a decimal 1. If both of its operands are false, a false value is returned i.e., a decimal 0.

# /*PROG 3.9 DEMO OF LOGICAL OR OPERATOR (||)*/

```
#include <iostream.h>
void main()
{
int res, a= 100, b=120;
res=(a>= 100 || b<0);
cout << "Returned value in res= " << res << endl;
}
```

# OUTPUT :

Returned value in res= 1

![](bbox=[0.28, 0.7, 0.72, 0.78])

Figure 3.9. Output screen of program.

EXPLANATION : The || is called OR operator. On both side of this operator condition is specified. If any of the condition is true the returned value is true that is 1 else 0. In the above program first condition in the expression is true but second is false so res contains 1 as result.