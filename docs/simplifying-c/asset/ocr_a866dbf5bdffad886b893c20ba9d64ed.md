```
#else
i_result = 1000 / (i_num * i_num * i_num);
#endif

printf("The result is %d. \n", i_result);
return;
}
```

**Output:**

```
The result is 1.
```

Similar to **#ifdef** directive, **#ifndef** directive can also be used within C programs. Program 13 illustrates the usage of **#ifndef** directive to check that whether or not macro TRUE is already defined. There is a chance of TRUE being defined as we have included the stdio.h header file. Thus, we would like to define macro named TRUE only if it is undefined.

**▶ Program 13**

```
/ * Program to illustrate the usage of #ifndef directive */

#include <stdio.h>

#ifndef TRUE
#define TRUE 1
#endif

main()
{
#ifndef TRUE
printf("The value of TRUE is %d\n", TRUE);
#endif

return;
}
```

**Output:**

```
The value of TRUE is 1
```

# **15.6 #error Directive**

The **#error** directive is used to diagnose compile time error messages and generate meaningful messages during debugging. The general syntax for **#error** directive is as follows:

```
#error error_message
```

When the **#error** directive is encountered, the error message specified in a program is displayed. Let us write a program to print a table of a number specified by a user. Programmer uses macro named MAX to decide number of iterations for printing table. For example, if MAX is 5 and i_num is 3, 5 iterations will be printed. Therefore, the last iteration will be 3 * 5 = 15.