TestExpr evaluates to true then statement1 will be executed. Consider the following C program with a dangling else problem.

```
#include <stdio.h>
int main()
{
    int a = 2;
    int b = 2;
    if (a == 1)
        if (b == 2)
            printf("a was 1 and b was 2\n");
        else
            printf("a wasn't 1\n");
    return 0;
}
```

When compiled and run, this program did not produce any output. With the program in its original form it is quite likely that the programmer thought the else statement

```
else
    printf("a wasn't 1\n");
```

would be associated with the first if but it was not. An else always associates with the immediately preceding if as is clear by the alternative version of the program. The reason for the complete absence of output is that there is no else statement associated with the first if.

In order to achieve the effect that the programmer probably originally intended, it is necessary to re-arrange the program in the following form.

```
int main()
{
    int a = 2;
    int b = 2;
    if (a == 1)
    {
        if (b == 2) printf("a was 1 and b was 2\n");
        else printf("a wasn't 1\n");
    }
    return 0;
}
```

# Note

+   - Multi-way decision statements are used to evaluate a test expression that could have several possible values.
+   - An else is always associated with the closest unmatched if.

# Check Your Progress

1. What will be the output of the following programs?

```
(a) int main()
    {
        printf("Hi!");
        if(-1)
```

```
            printf("Bye");
        return 0;
    }
```

Output Hi!Bye

```
(b) int main()
    {
        printf("Hi!");
        if(1)
            printf("Bye");
        return 0;
    }
```

Output Hi!

```
(c) float x = 199.9;
    if( x < 100)
        printf("one ");
    if(x < 200)
        printf("two ");
    if(x < 300)
        printf("three ");
```

Output two three

```
(d) int main()
    {
        int i= -1;
        unsigned int j =1;
        if(i<j)
            printf("Less");
        else
            printf("Greater");
        return 0;
    }
```

Output Greater

# 10.4.2 The Conditional Operator

Consider the situation in which there are two or more alternatives for an expression. Such a situation arises frequently in programming. For example, depending on existing conditions, there may be two or more alternative values evaluated from the expression. There may be two or more alternative expressions, based on existing conditions, for the value to be returned by a specific function. There may be two or more alternative expressions, again based on existing conditions, for the value of a specific argument in a function call. The conditional operator of C is specifically tailored for such situations. It has the following simple format:

```
expr1 ? expr2 : expr3
```

It executes by first evaluating expr1, which is normally a relational expression, and then evaluates either expr2, if the first result was true, or expr3, if the first result was false.