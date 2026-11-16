# 25. Omitting return type declarations

Omitting the return type of a function is a syntax error, if the function returns any other value other than int.

For example,

```
abc = sum (a) ;
```

If the return type for a function is not declared explicitly then the compiler will assume that is function returns a value of type int. Hence, it is a good programming practice to use void as a return type.

# 26. Mismatch of arguments in the function definitions and the function call

It's a syntax error to call a function, which doesn't match with the arguments present in function definition or function declaration.

# 27. Defining a function inside another function

It's a syntax error to define a function inside another function. However, you can call a function from any other function.

# 28. Confusing the operator (->) with the operator(.) when referencing structure variables.

Note that, the dot or period operator (.) is used for structure variables, while the arrow operator -> is used for structure pointer variables. So if 'a' is a structure variable then the notation a.b is used to refer the member b of a, where as if 'a' is a pointer to a structure, then the notation a -> b is used to refer the member b of the structure pointed to by b.

# 29. Leaving a blank space between the name of a macro and its argument list in the #define statements

For example,

```
#define PAY (m, n) (30, 80)
```

The above macro definition is incorrect, as the preprocessor considers the first blank space after the defined name as the start of the definition of that name.

The definition should be

```
# define PAY(M, N) (30, 80)
```

# 30. Omitting parenthesis around arguments in macro definition

```
#define SQR(x) x * x
main()
{
 int y;
 y = 16/SQR(4);
 printf("%d", y);
}
```

In the above example we would expect the value of y to be 1, but the value will be 16. this happens because on preprocessing the arithmetic statements takes the form of

```
y = 16 / 4 * 4 ;
```

the arithmetic statement should be

```
y = 16/(SQR(4));
```