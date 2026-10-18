# DISPLAY 4.16 Factorial Function

# Function Declaration

```
1    int factorial(int n);
2    //Returns factorial of n.
3    //The argument n should be nonnegative.
```

# Function Definition

```
1    int factorial(int n)
2    {
3        int product = 1;
4        while (n > 0)
5        {
6            product = n * product;
7            n--;
8        }
9
10       return product;
11   }
```

formal parameter n used as a local variable

The function definition for factorial uses two local variables: product, which is declared at the start of the function body, and the formal parameter n. Since a formal parameter is a local variable, we can change its value. In this case we change the value of the formal parameter n with the decrement operator n--. (The decrement operator was discussed in Chapter 2.)

Each time the body of the loop is executed, the value of the variable product is multiplied by the value of n, and then the value of n is decreased by one using n--. If the function factorial is called with 3 as its argument, then the first time the loop body is executed the value of product is 3, the next time the loop body is executed the value of product is 3 * 2, the next time the value of product is 3 * 2 * 1, and then the while loop ends. Thus, the following will set the variable x equal to 6 which is 3 * 2 * 1:

```
x = factorial(3);
```

Notice that the local variable product is initialized to the value 1 when the variable is declared. (This way of initializing a variable when it is declared was introduced in Chapter 2.) It is easy to see that 1 is the correct initial value for the variable product. To see that this is the correct initial value for product, note that after executing the body of the while loop the first time, we want the value of product to be equal to the (original) value of the formal parameter n; if product is initialized to 1, then this will be what happens.

Formal parameter used as a local variable