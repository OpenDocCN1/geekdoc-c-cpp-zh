# DISPLAY 16.5 Throwing an Exception Inside a Function (part 2 of 2)

# Sample Dialogue 1

```
Enter numerator:
5
Enter denominator:
10
5/10 = 0.5
End of Program.
```

# Sample Dialogue 2

```
Enter numerator:
5
Enter denominator:
0
Error: Division by zero!
Program aborting.
```

This statement is not visible in the try block. However, it is in the try block in terms of program execution, because it is in the definition of the function safeDivide and there is an invocation of safeDivide in the try block.

# Exception Specification

If a function does not catch an exception, it should at least warn programmers that any invocation of the function might possibly throw an exception. If there are exceptions that might be thrown, but not caught, in the function definition, then those exception types should be listed in an exception specification, which is illustrated by the following function declaration from Display 16.5:

```
double safeDivide(int top, int bottom) throw (DivideByZero);
```

As illustrated in Display 16.5, the exception specification should appear in both the function declaration and the function definition. If a function has more than one function declaration, then all the function declarations must have identical exception specifications. The exception specification for a function is also sometimes called the throw list.

If there is more than one possible exception that can be thrown in the function definition, then the exception types are separated by commas, as illustrated here:

```
void someFunction( ) throw (DivideByZero, OtherException);
```