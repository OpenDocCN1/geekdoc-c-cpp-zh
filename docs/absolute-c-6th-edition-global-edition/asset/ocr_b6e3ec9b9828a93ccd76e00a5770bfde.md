As we noted earlier, you can always assign a value of an integer type to a variable of a floating-point type, as in

```
double d = 5;
```

In such cases C++ performs an automatic type cast, converting the 5 to 5.0 and placing 5.0 in the variable d. You cannot store the 5 as the value of d without a type cast, but sometimes C++ does the type cast for you. Such an automatic conversion is sometimes called a type coercion.

type coercion

# Increment and Decrement Operators

The ++ in the name of the C++ language comes from the increment operator, ++. The increment operator adds 1 to the value of a variable. The decrement operator, --, subtracts 1 from the value of a variable. They are usually used with variables of type int, but they can be used with any numeric type. If n is a variable of a numeric type, then n++ increases the value of n by 1 and n-- decreases the value of n by 1. So n++ and n-- (when followed by a semicolon) are executable statements. For example, the statements

increment operator

decrement operator

```
int n = 1, m = 7;
n++;
cout << "The value of n is changed to " << n << "\n";
m--;
cout << "The value of m is changed to " << m << "\n";
```

yield the following output:

```
The value of n is changed to 2
The value of m is changed to 6
```

An expression like n++ returns a value as well as changing the value of the variable n, so n++ can be used in an arithmetic expression such as

```
2* (n++)
```

The expression n++ first returns the value of the variable n, and then the value of n is increased by 1. For example, consider the following code:

```
int n = 2;
int valueProduced = 2* (n++);
cout << valueProduced << "\n";
cout << n << "\n";
```

This code will produce the output

```
4
3
```

Notice the expression 2* (n++). When C++ evaluates this expression, it uses the value that number has before it is incremented, not the value that it has after it is incremented. Thus, the value produced by the expression n++ is 2, even though the increment operator changes the value of n to 3. This may seem strange, but sometimes it is just