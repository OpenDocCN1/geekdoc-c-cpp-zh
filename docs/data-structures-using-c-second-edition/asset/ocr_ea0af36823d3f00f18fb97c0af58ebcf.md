```
printf("\n The value of num after calling the function = %d", num);
return 0;
}
void add(int n)
{
    n = n + 10;
    printf("\n The value of num in the called function = %d", n);
}
```

# Output

The value of num before calling the function = 2
The value of num in the called function = 12
The value of num after calling the function = 2

Following are the points to remember while passing arguments to a function using the call-by-value method:

+   - When arguments are passed by value, the called function creates new variables of the same data type as the arguments passed to it.
+   - The values of the arguments passed by the calling function are copied into the newly created variables.
+   - Values of the variables in the calling functions remain unaffected when the arguments are passed using the call-by-value technique.

# Pros and cons

The biggest advantage of using the call-by-value technique is that arguments can be passed as variables, literals, or expressions, while its main drawback is that copying data consumes additional storage space. In addition, it can take a lot of time to copy, thereby resulting in performance penalty, especially if the function is called many times.

# Call by Reference

When the calling function passes arguments to the called function using the call-by-value method, the only way to return the modified value of the argument to the caller is explicitly using the return statement. A better option is to pass arguments using the call-by-reference technique. In this method, we declare the function parameters as references rather than normal variables. When this is done, any changes made by the function to the arguments it received are also visible in the calling function.

To indicate that an argument is passed using call by reference, an asterisk (*) is placed after the type in the parameter list.

Hence, in the call-by-reference method, a function receives an implicit reference to the argument, rather than a copy of its value. Therefore, the function can modify the value of the variable and that change will be reflected in the calling function as well. The following code illustrates this concept.

```
#include <stdio.h>
void add(int *);
int main()
{
    int num = 2;
    printf("\n The value of num before calling the function = %d", num);
    add(&num);
    printf("\n The value of num after calling the function = %d", num);
    return 0;
}
void add(int *n)
```