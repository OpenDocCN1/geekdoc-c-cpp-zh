But the post- and pre-operations play a different role when they are specified in the *test_expression*.

```
#include <stdio.h>
int main()
{
    int c;
    for(c=0; c++; c++)
        printf("%d", c);
    return 0;
}
```

**Output** Prints nothing as c has been initialized as zero and the post-increment of c makes a difference. The condition is evaluated first, followed by increment. The condition is evaluated false as c contains zero at that moment. The printf() statement will not be executed as the condition becomes false.

```
#include <stdio.h>
int main()
{
    int c;
    for(c=0; ++c; ++c)
        printf("%d", c);
    return 0;
}
```

**Output** This is an infinite loop. As the first pre-increment takes place, it results in c=1. Then the test expression evaluates to 1 as c contains a non-zero value. Thus the loop continues.

+   * It is possible to have a variable increase by a value other than one. For example, the following loop would iterate four times with the variable num taking on the values 1, 4, 7, and 10. The step expression adds 3 to the value of num on each iteration.

```
for(num = 1; num <= 10; num = num + 3)
```

It is a common error for students to use the following for statement, which causes a compilation error:

```
for(num = 1; num <= 9 ; num + 3)
```

Consider the following program where the increment operator is used at a place other than the third part of the for statement.

```
#include <stdio.h>
int main()
{
    int c;
    for(c=1; c<=5; )
        printf("%d", c++);
```

```
    return 0;
}
```

Output 12345

```
#include <stdio.h>
int main()
{
    int c;
    for(c=1; c<=5;)
        printf("%d", ++c);
    return 0;
}
```

Output 23456

+   * Any or all of the three expressions in a for loop can be omitted, but the two semicolons must remain. When all three expressions in a for loop are omitted, it acts as a infinite loop. For example,

```
for(;;)
{
    printf("hello\n");
}
```

This loop will run forever. Although there are some programming tasks, such as operating system command processors, which require an infinite loop, most ‘infinite loops’ are really just loops with special termination requirements.

+   * Often, the variable that controls a for loop is needed only for the purposes of the loop and is not used elsewhere. When this is the case, it is possible to declare the variable inside the initialization portion of the for loop in modern compiler. Some compilers, however, do not. You will need to check this feature in the environment you are using. Consider the following program which prints the sum of the following series

```
#include <stdio.h>
int main()
{
    int s=0, n;
    printf("\n Enter the No. of terms");
    scanf("%d", &n);
    for(int c=1; c<=n; c++)
    s+=c;
    printf("\n Sum is %d", s);
    return 0;
}
```

![](bbox=[0.74, 0.79, 0.9, 0.83])

The variable c is only known throughout the execution of the for loop (it's called a local variable) and cannot