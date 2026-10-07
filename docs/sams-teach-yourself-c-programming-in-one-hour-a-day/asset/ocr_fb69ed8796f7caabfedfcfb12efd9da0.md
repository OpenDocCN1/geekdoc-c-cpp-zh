# LESSON 19 Getting More from Functions

# FIGURE 19.2 half(&x); x

Passing by reference enables the function to modify the original argument's variable.

![](bbox=[0.273, 0.146, 0.847, 0.435])

The function used in Figure 19.2 is not a good example of a real program in which you would pass by reference, but it does illustrate the concept. When you pass by reference, you must ensure that the function definition and prototype reflect that the argument passed to the function is a pointer. Within the body of the function, you must also use the indirection operator to access the variable(s) passed by reference.

Listing 19.1 demonstrates passing by reference and the default passing by value. Its output clearly shows that a variable passed by value can't be changed by the function, whereas a variable passed by reference can be changed. Of course, the function doesn't need to modify a variable passed by reference. In such a case, there's no reason to pass by reference.

# Input

# LISTING 19.1 differentarguments.c: Passing by Value and Passing by Reference

```
1:    // differentarguments.c--Passing arguments by value and by reference. *
2:
3:    #include <stdio.h>
4:
5:    void by_value(int a, int b, int c);
6:    void by_ref(int *a, int *b, int *c);
7:
8:    int main( void )
9:    {\{
10:       int x = 2, y = 4, z = 6;
11:
```