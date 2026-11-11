The 'return' statement will return the result of addition as 30 back to the main() function which will be initialized to the variable c as shown in Figure 7.24.

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

calls the function add() one more time by passing the hardcoded values 100 and 200 and storing the result of addition in variable d. This means that the function add() will again be executed (with a new activation frame) by setting the values of formal arguments 'p' and 'q' as 100 and 200, respectively. Therefore, add() will return the result of addition as 300 which will be initialized to the variable d.

# What is a return type?

The return type of the function is the data type of a value returned by the function. In the above example, the function add() returns addition of two integers which is also a integer, and hence its return type is int. To clarify further, consider function f1() which returns value of a as shown below. In this case the return type of the function f1() must be specified as **float** because the data type of variable a is float

```
float f1()
{
float a;
-------------
-------------
return a;
}
```

# What will happen if, we do not specify the return type of a particular function in the program?

If we do not specify the return type its by default considered as int by the compiler. For example if we define a function f1() without specifying any return type as follows:

```
f1()
{
-------------
-------------
}
```

then, the compiler expects f1() to return an integer.