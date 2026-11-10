```
void (*fp1)();
fp1 = print_something;
print(fp1);
```

We have been able to pass the simplest function pointer as an argument to another function. How does one pass the **add** function with its two arguments to another function, say, **compute**? It is here that function pointers can get a little confusing, but it need not be so if you have a re-look at the declaration of the **print** function. The following declaration for the **compute** function uses three arguments, one for the **add** function itself and two for its arguments:

```
float compute(float (*fp)(float, float), float x, float y);
```

The declaration tells the compiler that the first parameter is a pointer to a function that accepts two float arguments and returns a float. This matches the prototype of the **add** function. The remaining two parameters represent the actual arguments of the function whose pointer is passed as the first argument. We can now call either **add** or fp2 from the **compute** function:

```
float (*fp2)(float, float);
fp2 = add;
printf("Result = %.2f\n", compute(fp2, 100, 200));
```

This prints the sum of 100 and 200, i.e. 300.00. Observe that even though we could run fp2 directly in the previous program as

```
result = (*fp2)(4.5, 5.5);
```

we can't pass this function call as a *single* argument to **compute**. The arguments used with fp2 have to be passed separately. If you appreciate and remember this feature, then you'll have no problem in handling callback functions. The observations we have just made are demonstrated in Program 17.5.

> **Takeaway:** If function f2 having n arguments is passed as an argument to function f1, then f1 must be declared with at least n + 1 arguments. The first argument of f1 represents f2, and the remaining ones represent the arguments of f2. The words “at least” are used because f1 may have other arguments that are not related to f2.

```
/* callback_func.c: Uses callback functions with or without
   arguments and return value. */
#include <stdio.h>

void (*fp1)();                  /* Declaration of function pointer fp1 */
void print_something();         /* Callback function */
void print(void (*fp)());       /* Meant to call a callback function */
float (*fp2)(float, float);     /* Declaration of function pointer fp2 */
float add(float x, float y);    /* Callback function */

/* Following function is meant to call a callback function. */
float compute(float (*fp)(float, float), float x, float y);
```