# 6.10 More About Function Declaration

The main thing about the placing of function declaration is that it should be before the function call. Generally all the function declarations are written before the main() function. This way the function declaration is accessible to all functions. It is also possible that we declare the function only inside those functions that call it. Note that if function definition occurs before the function call, then declaration is not needed.

If a function returns a value of type int or char then it is not necessary to declare the function, because by default every function returns an int value. The compiler assumes that any function, for which return type is not specified in the definition, will return an int value. But if the function returns a value other than int such as float, double, pointer, array, structure etc then it is necessary to declare it before the function call.

Declaration of a function has two main uses. Firstly, it tells the compiler about the return type of the function. Secondly, it specifies the type and number of arguments of the function. So it can be used to check any mismatch between the number and type of arguments in the function definition and function call. We had seen that it is optional to declare the functions of type int or char, but it is a good practice to declare all functions since we can check the number and type of arguments in function call. So in this way we can prevent bugs, which could occur due to wrong number and type of arguments in the function call.

# 6.11 Declaration Of Functions With No Arguments

If a function has no arguments, then either the parentheses can be left empty or void can be written inside the parentheses. But it is better to write void because when parentheses are empty, the compiler assumes that there is no information about the arguments. There can be no arguments or any number of arguments. So the compiler won't be able to check any mismatch in the type and number of arguments in function call.

Similarly void can be specified as return type if a function does not return any value. This will avoid accidental use of function in any expression. For example-

```
/*P6.15 Program to understand declaration of functions with no arguments*/
#include<stdio.h>
void func1();
void func2(void);
main()
{
    func1(1.3,'a'); /*will not generate any error*/
    func2(1.3,'a'); /*will generate error*/
}
void func1()
{
    printf("\nFunction1\n");
}
void func2(void )
{
    printf("\nFunction2\n");
}
```

Here we see that func1() can be called with wrong number and type of arguments and it will not show