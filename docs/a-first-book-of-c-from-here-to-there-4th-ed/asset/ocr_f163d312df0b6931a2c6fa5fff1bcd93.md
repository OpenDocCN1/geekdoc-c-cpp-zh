This is the output produced by Program 6.13:

```
The value of the automatic variable num is 0
The value of the automatic variable num is 0
The value of the automatic variable num is 0
```

Each time testauto() is called, the auto variable num is created and initialized to 0. When the function returns control to main(), the variable num is destroyed along with any value stored in num. Therefore, the effect of incrementing num in testauto(), before the function's return statement, is lost when control is returned to main().

For most applications, the use of auto variables works just fine and is the reason it's the default storage category. In some cases, however, you want a function to remember values between function calls, which is the purpose of the static storage category. A local variable declared as static causes the program to keep the variable and its latest value even when the function that declared it has finished executing. The following are examples of static variable declarations:

```
static int rate;
static double amount;
static char inKey;
```

A local static variable isn't created and destroyed each time the function declaring it is called. After they're created, local static variables remain in existence for the program's lifetime. This means the last value stored in the variable when the function finishes executing is available to the function the next time it's called.

Because local static variables retain their values, they aren't initialized in a declaration statement in the same way as auto variables. To understand why, consider the auto declaration int num = 0;, which causes the auto variable num to be created and set to 0 each time the declaration is encountered. This procedure is called a runtime initialization because initialization occurs each time the declaration statement is encountered. This type of initialization would be disastrous for a static variable because resetting the variable's value to 0 each time the function is called destroys the very value you're trying to save.

Initialization of static variables (both local and global) is done only once, when the program is first compiled. At compile time, the variable is created and any initial value is placed in it. Thereafter, the value in the variable is kept without further initialization. To see how this process works, examine Program 6.14.