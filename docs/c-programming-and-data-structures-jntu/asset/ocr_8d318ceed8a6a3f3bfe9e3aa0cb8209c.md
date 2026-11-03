# 10.3 C Programming and Data Structures

When the function references the variable count, it will be referencing only its local variable, not the global one. The value of count in main will not be affected.

# Example 10.8

A program to illustrate the properties of global variables is presented in Fig. 10.14. Note that variable x is used in all functions, but none except fun2, has a definition for x. Because x has been declared ‘above’ all the functions, it is available to each function without having to pass x as a function argument.

```
Program
/**************************************************
* ILLUSTRATION OF PROPERTIES OF GLOBAL VARIABLES *
**************************************************/

int x;

main()
{
	x = 10;
	printf("x=%d\n", x);
	printf("x=%d\n", fun1());
	printf("x=%d\n", fun2());
	printf("x=%d\n", fun3());
}

fun1()
{
	x = x + 10;
	return(x);
}

fun2()
{
	int x;
	x = 1;
	return(x);
}

fun3()
{
	x = x + 10;
	return(x);
}

Output

x = 10
x = 20
x = 1
x = 30
```

Fig. 10.14 Illustration of global variables

Once a variable has been declared as global, any function can use it and change its value. Then, subsequent functions can reference only that new value. Because of this property, we should try to use global variables only for tables or for variables shared between functions when it is inconvenient to pass them as parameters.