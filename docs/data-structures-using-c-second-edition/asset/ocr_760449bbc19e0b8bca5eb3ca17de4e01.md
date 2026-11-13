```
{
*n = *n + 10;
printf("\n The value of num in the called function = %d", n);
}
```

# Output

The value of num before calling the function = 2
The value of num in the called function = 12
The value of num after calling the function = 12

# Advantages

The advantages of using the call-by-reference technique of passing arguments include:

+   - Since arguments are not copied into the new variables, it provides greater time and space-efficiency.
+   - The function can change the value of the argument and the change is reflected in the calling function.
+   - A function can return only one value. In case we need to return multiple values, we can pass those arguments by reference, so that the modified values are visible in the calling function.

# Disadvantages

However, the drawback of using this technique is that if inadvertent changes are caused to variables in called function then these changes would be reflected in calling function as original values would have been overwritten.

Consider the code given below which swaps the value of two integers. Note the value of integers in the calling function and called function.

```
//This function swaps the value of two variables
#include <stdio.h>
void swap_call_val(int, int);
void swap_call_ref(int *, int *);
int main()
{
 int a=1, b=2, c=3, d=4;
 printf("\n In Main(), a = %d and b = %d", a, b);
 swap_call_val(a, b);
 printf("\n In main(), a = %d and b = %d", a, b);
 printf("\n\n In main(), c = %d and d = %d", c, d);
 swap_call_ref(&c, &d);
 printf("\n In main(), c = %d and d = %d", c, d);
 return 0;
}
void swap_call_val(int a, int b)
{
 int temp;
 temp = a;
 a = b;
 b = temp;
 printf("\n In Function (Call By Value Method) - a = %d and b = %d", a, b);
}
void swap_call_ref(int *c, int *d)
{
 int temp;
 temp = *c;
 *c = *d;
 *d = temp;
 printf("\n In Function (Call By Reference Method) - c = %d and d = %d", *c, *d);
}
```