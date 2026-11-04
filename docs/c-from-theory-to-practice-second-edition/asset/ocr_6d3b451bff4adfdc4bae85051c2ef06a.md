**Comments:** The preprocessor expands the macros from the inner to the outer. Notice, that there are other alternatives, for example, we could write `max(max(1, j), max(k, 1));`.

**C.16.10** Write a macro that can read an integer, a float, or a character and display it. Write a program that uses this macro to read an integer, a float, and a character in that order and display their values.

```
#include <stdio.h>

#define f(type, text, a) printf(text); scanf(type, &a); printf(type"\n",
a);

int main(void)
{
    char ch;
    int i;
    float fl;

    f("%d", "Enter integer: ", i);
    f("%f", "Enter float: ", fl);
    f(" %c", "Enter character: ", ch); /* Insert a space, so that
    scanf() ignores white space. */
    return 0;
}
```

**C.16.11** What is the output of the following program?

```
#include <stdio.h>

#define no_main(type, name, text, num) type name(void) { printf(text);
return num; }

no_main(int, main, "No main()", 0)
```

**Answer:** Leave the best for the end. “Silver alert,” main() is lost. The program works, though. The preprocessor replaces `type` with `int`, `name` with `main`, `text` with "No main()" and `num` with `0`. Therefore, the preprocessor expands `no_main()` to:

```
int main(void) { printf("No main()"); return 0; }
```

and the program displays: No main()

Notice that if we were using `void` instead of `int` the compilation would fail, because a `void` function cannot return a value.

# ## Unsolved Exercises

**U.16.1** Write a macro that checks whether a number is between two other numbers. Write a program that reads three numbers (e.g., `x`, `a`, `b`) and uses the macro to check if `x` is within `[a, b]`.