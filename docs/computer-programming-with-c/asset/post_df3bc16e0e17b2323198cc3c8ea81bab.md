
## Order of arguments specified in the function call to `sub()`

The values of actual arguments will be assigned to the formal arguments with an associativity of **Left to Right**.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_332_0.png)

Figure 7.21: Calling the function `sub()`

## Specifying direct values at the time of a function call

We can pass constant values at the time of a function call. For example, the values 400 and 100 can be passed to the function `add()` using the following function call:

![](img/57c0d966bb33c67a5a188e6bf39e4e02_332_1.png)

Figure 7.22: Calling the function `add()`

This function call passes the hardcoded argument values as 400 and 100 to the function `add()`. This means that the function `add()` will be ‘called’ one more time and the actual arguments 400 and 100 will be initialized to the formal arguments p and q as shown in Figure 7.22. Hence, the result of addition will now be calculated as **500** which is shown in Figure 7.22.

## NOTES

Be careful when you decide the order of arguments. Remember that the data type of each of the actual arguments must match with the data type of corresponding formal arguments. In our case, both the data types of `add()` and `sub()` were of type integer so we never bothered about data types of arguments while deciding their order. If the function `add()` is defined in such a way that the first argument is of type `float` and the second argument is of type `int` then it is programmers’ responsibility to make sure that the data type of first argument being passed to it is `float` and second is `int`. In many cases, C/C++ can perform implicit type conversions when data types do not match, but it may result in truncation of data. For example, if `float` value is passed to an `int` argument, everything after decimal point will be truncated. Although the compiler will not complain, it is not really a good programming practice to truncate the results. Hence, you should always try to ensure that the data type of each of the actual arguments must match with the data type of corresponding formal arguments when working with primitive types.

## CONSTANT ARGUMENTS

In this case, the functions `add()` and `sub()` take arguments but they do not modify the value of these arguments. For example, `add()` accepts arguments p and q but its functionality is not really to modify the values of p and q but just perform addition of p and q and generate a third value. In such situations, you can create an argument as a constant argument by adding a keyword `const` before the argument while defining the function

```
void add( const int p , const int q)
{
/*Function body*/
int res = p+q; /*Works fine*/
p=p+1; /*ERROR! Cannot modify constant argument*/
q=q+1; /*ERROR! Cannot modify constant argument*/
    ..
    ..
}
```

Adding keyword `const` conveys to the compiler that these arguments will not change their values in the function definition. This protects the genuine programmers from making accidents by modifying the value of a variable passed as an argument instead of some other variable. The compiler will give an error if any of the arguments which are marked as `const` are modified. If you mark arguments of function as `const`, you must also add keyword `const` in the function prototype as well. For example, if both the arguments of `add()` are marked as `const`, then the prototype of `add()` must be as follows:

```
void add(const int, const int);
```

The real use of `const` arguments is when a function is called by reference which we will learn in Chapter 8.

## 7.5 Functions with Return Values

The ‘called’ function can give a single value back to the ‘calling’ function. This value sent from the ‘called’ function to the ‘calling’ function is called a ‘return value’. The ‘return value’ typically represents the result of the operations performed by the ‘called’ function.

The ‘return’ statement in C/C++ is used to send a value back to the caller. Given below is the syntax of the return statement:

```
return <expression>;
```

The statement will return the result of the expression back to the calling function.

> **NOTES**
> 
> We can only return one value at a time from the called function to the calling function.

As an example to demonstrate the usage of the return statement, let us write a function add() that performs the addition of two arguments passed to it and returns back the result of the addition to the ‘calling’ function. If two formal arguments p and q store the values to be added, the statement

```
return p+q;
```

will return the result of p+q to the caller. As the arguments p and q are of type int, the result will also be an integer. As add() returns an integer value, the prototype datatype is as shown in Figure 7.23.

This means that the function add() takes two arguments of type int and returns one value of type int. Given below is the source code that creates a function add() returning the result of addition of two integers to the main() function.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_334_0.png)

```
#include<stdio.h>
int add(int,int);
void main()
{
int a,b,c;
printf("Enter the values of a and b\n");
scanf("%d%d",&a,&b);
c=add(a,b);
printf("Addition of %d and %d is %d\n",a,b,c);
int d;
d= add(100,200);
printf("Addition of 100 and 200 is %d\n",d);
}
int add(int p,int q)
{
return p+q;
}
```

### Output

```
Enter the values of a and b
10 20
Addition of 10 and 20 is 30
Addition of 100 and 200 is 300
```

As the execution always starts from the main() function, we will trace the output of the program starting from the first statement of main().

The statements

```
int a,b,c;
printf("Enter the values of a and b\n");
scanf("%d%d",&a,&b);
```

create the local variables a, b and c inside the main() function, accepting the values of variables a and b as input from the user. Let the user input the values of a and b as 10 and 20, respectively.

The statement

```
c = add(a,b);
```

calls the function add() by passing the values of a and b as arguments. The value of variable c will be initialized with the value returned by add() as shown in Figure 7.24. As we have assumed the values of variables a and b to be 10 and 20, respectively, the value of the formal argument p will be set to 10 and the value of the formal argument q will be set to 20.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_335_0.png)

The ‘return’ statement will return the result of addition as 30 back to the main() function which will be initialized to the variable c as shown in Figure 7.24.

The main() function prints the result of addition using the printf statement

```
printf("Addition of %d and %d is %d\n",a,b,c);
```

As the value of c is initialized to 30, the output of the statement is

```
Addition of 10 and 20 is 30
```

The next statement

```
d=add(100,200) ;
```

calls the function add() one more time by passing the hardcoded values 100 and 200 and storing the result of addition in variable d. This means that the function add() will again be executed (with a new activation frame) by setting the values of formal arguments ‘p’ and ‘q’ as 100 and 200, respectively. Therefore, add() will return the result of addition as 300 which will be initialized to the variable d.

### What is a return type?

The return type of the function is the data type of a value returned by the function. In the above example, the function add() returns addition of two integers which is also an integer, and hence its return type is int. To clarify further, consider function f1() which returns the value of a as shown below. In this case, the return type of the function f1() must be specified as **float** because the data type of variable a is float.

```
float f1()
{
float a;
-------------
-------------
return a;
}
```

### What will happen if we do not specify the return type of a particular function in the program?

If we do not specify the return type, it is by default considered as `int` by the compiler. For example, if we define a function f1() without specifying any return type as follows:

```
f1()
{
-------------
-------------
}
```

then, the compiler expects f1() to return an integer.
