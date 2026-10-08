
Enter marks scored in English, Maths and Science: 50 40 40
Total marks scored is 130

In Program 8, we have defined two macros, namely, MARKS and PLUS. When Program 8 is preprocessed, MARKS will be replaced by int and PLUS will be replaced by +. Thus, the data type variables i_eng, i_math, and i_sci become integers. The statement i_total = i_eng PLUS i_math PLUS i_sci will be converted to i_total = i_eng + i_math + i_sci because of the replacement of PLUS with the + operator. The converted statement is a valid C statement. Therefore, it is compiled and executed successfully.

The macros that we have discussed till now did not contain any arguments. C language has made a provision to define macro with arguments. The next section discusses how a macro can be defined along with its arguments.

## Macros with Arguments

In Chapter 8 we learned that functions can accept arguments. The arguments were classified as actual arguments or formal arguments. Similar to functions, macros can also accept arguments. The arguments of macro are also classified as actual or formal. A macro call substitutes the formal arguments of the macro body with actual arguments passed during macro call. Macros that accept arguments are also called macro functions. Program 9 illustrates the usage of macros with arguments:

▶ Program 9

```c
/* Program to illustrate macros with arguments */

#include<stdio.h>
#define SI(p, r, n) ((p * r * n) / 100)

main()
{
	int i_principal, i_duration;
	float f_si, f_roi;

	printf("\n Enter Principal amount: ");
	scanf("%d", &i_principal);
	printf("\n Enter Rate of interest: ");

	scanf("%f", &f_roi);
	printf("\n Enter Duration: ");
	scanf("%d", &i_duration);

	f_si = SI(i_principal, f_roi, i_duration);
	printf("\n Calculated Simple Interest is : %0.2f \n", f_si);
	return;
}
```

Output:

Enter Principal amount: 1000
Enter Rate of interest: 10
Enter Duration: 1
Calculated Simple Interest is : 100.00

In Program 9, we have defined a macro named SI with three arguments, namely, Principal amount (p), Rate of Interest (r), and Duration of deposit (n). The macro body contains the expression ((p * r * n )/100). The statement f_si = SI(i_principal, f_roi, i_duration) will be converted to f_si = ((i_principal * f_roi * i_duration) /100) by the preprocessor before sending it to the translator. This replacement of the macro body is termed as macro call, as it is not simple replacement, but replacement with argument value substitution.

Be careful not to leave blank between macro name and opening braces containing arguments. For example, no space should be left between SI and (p, r, n) in the definition #define SI(p, r, n) ((p * r * n ) / 100). In case we leave a blank space between the macro name and its arguments, say, #define SI (p, r, n) ((p * r * n) / 100), the preprocessor will consider SI as the macro name and (p, r, n) ((p * r * n) / 100) as the macro body. This will lead to unexpected results or compilation errors.

Macro shares one common property with the C functions. Similar to C functions, macros can also be nested. Program 10 illustrates nested macro:

▶ Program 10

```c
/* Program to illustrate nested macros */

#include<stdio.h>
#define TRUE 1
#define FALSE 0
#define ISEVEN(i_x) ((i_x%2) == 0? TRUE : FALSE)

main()
{
    int i_num;
    printf("\n Enter number : ");
    scanf("%d", &i_num);

    if ISEVEN(i_num)
       printf("The number is even\n");

    else
       printf("The number is odd\n");

    return;
}
```

Output 1:

Enter number : 5
The number is odd

Output 2:

Enter number : 6
The number is even

Program 10 will be preprocessed in two steps: first, at the time of preprocessing, the preprocessor replaces 1 wherever it finds the macro name TRUE. Similarly, FALSE is replaced by 0. Thus, the statement #define ISEVEN(i_x) ((i_x%2) == 0 ? TRUE : FALSE ) will be converted to #define ISEVEN(i_x) ((i_x%2) == 0 ? 1 : 0). Observe that the macros TRUE and FALSE have been used within the macro ISEVEN, and this property is termed as macro nesting.

In the next step, the preprocessor expands the macro name ISEVEN to ((i_x%2) == 0 ? 1 : 0). Along with the expansion, the preprocessor also replaces with the required parameters passed while calling a macro. In Program 10, variable i_num is passed as a parameter. Hence, i_x will be replaced by i_num. Thus, ISEVEN (i_num) will be replaced by ((i_num%2) == 0 ? 1 : 0)

Note that when macro expansion is to be used for calculations, the entire macro body should be enclosed within parentheses. Program 11 illustrates macro call leading to unexpected result, if we fail to enclose the macro body within parentheses:

Program 11

```c
/* Program to illustrate importance of enclosing macro body within parentheses*/
#include<stdio.h>
#define CUBE(i_x) i_x * i_x * i_x

main()
{
  int i_num = 10, i_result;

  i_result= 1000 / CUBE(i_num);
  printf("The result is %d \n", i_result);
  return;
}
```

Output:

The result is 10000

Program 11 intended to calculate 1000 divided by cube of 10. The expected result is 1. However, the result of the program as displayed is 10000. This happens as i_result = 1000 / CUBE(i_num); is converted to i_result = 1000/10 * 10 * 10 after preprocessing. According to the operator precedence rule, division and multiplication hold the same precedence level and are evaluated from left to right. Thus, 1000/10 is calculated first. This results into 100, and then the expression 100 * 10 * 10 is evaluated. Macros, though advantageous, can lead to unexpected results if not defined carefully. The next section discusses about the advantages of using macros.

## Advantages of Using Macros

Macros are very useful when replacement for a single macro is to be done at multiple places in a program. It increases the readability of the program. It is also very easy to modify the constant value as modification needs to be done at a single place. Suppose a constant like PI, which we have used in Program 3, appears multiple times in a single program. The value of PI is defined as 3.14. Now, it is decided to change the value of PI from 3.14 to 3.1415. If macro is used, these types of changes are to be done only at a single place. The convenience of changing a value at one place may not matter in small programs. However, in large programs, the usage of macros is almost inevitable. We can also use the variable PI = 3.14, instead of defining macro using the preprocessor directive. But it is not a good idea. Preprocessor replaces macro body wherever macro name is found throughout the program. This reduces the task of compiler. Thus, the compilation time is reduced at a large extent.

Macro allows us to write modular programs to certain extent. We can create a library of C macros similar to C functions. The next section discussed the differences between macro and functions.

## Macros versus Functions

We have seen macros with arguments in Programs 9, 10, and 11. The operation that we performed in these programs using macro could also be performed using functions. When we make a call to function, it is referred to as function call, while macro when called is termed as macro call. Both of them look alike; hence a question may arise whether it is better to use a macro or a function? If both are same, either can be used in any situation. However, though function calls and macro calls look alike, both of them are not same. There is a difference in their working. Table 2 describes the difference between macros and functions:

| Table 2: Macros versus Functions | |
| :--- | :--- |
| **Macro** | **Function** |
| Macro call is replaced by macro expansion while processing the source code by the preprocessor. Macros are faster and efficient than functions. | Whenever a function is called, the control is passed to the function along with the arguments. After the calculations are performed, control is returned back to the main function. |
| If a macro is called multiple times in a program, the macro body is replaced multiple times in a program. The size of the program may exceed if macros are used. | Program size remains compact even though the function call is made for several times in a program. |
| No address is associated with macro identifier, and hence pointers cannot be used with macros. | Functions have their own addresses defined, and hence pointers can be used. |
| When we pass the arguments to the macro, it never checks for their data types. It only checks for the number of arguments. | Function calls always check for data types as well as number of arguments. |

It is clear from Table 2 that macros are typically used to associate meaningful identifiers with constants, keywords, and commonly used statements or expressions. The choice between using a macro and using a function is decided between the tradeoff of faster program execution versus smaller program size. Generally, we should use macros to replace small, repeatable code sections. It avoids the overheads associated with function calls. We should use functions for larger coding tasks that might require several lines of code.

C language allows us to remove the definition of an existing macro. The next section shows us how a macro definition can be removed.
