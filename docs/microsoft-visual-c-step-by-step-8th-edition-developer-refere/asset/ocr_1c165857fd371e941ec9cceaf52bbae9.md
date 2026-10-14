and has a single int parameter, called answer:

```
void showResult(int answer)
{
    // ...
}
```

Notice the use of the keyword void to indicate that the method does not return anything.

# Important

If you’re familiar with Visual Basic, notice that C# does not use different keywords to distinguish between a method that returns a value (a function) and a method that does not return a value (a procedure or subroutine). You must always specify either a return type or void.

# Returning data from a method

If you want a method to return information (that is, its return type is not void), you must include a return statement at the end of the processing in the method body. A return statement consists of the keyword return followed by an expression that specifies the returned value and a semicolon. The type of the expression must be the same as the type specified by the method declaration. For example, if a method returns an int, the return statement must return an int; otherwise, your program will not compile. Here is an example of a method with a return statement:

Click here to view code image

```
int addValues(int leftHandSide, int rightHandSide)
{
    // ...
    return leftHandSide + rightHandSide;
}
```

The return statement is usually positioned at the end of the method because it causes the method to finish, and control returns to the statement that called the method, as described later in this chapter. Any statements that occur after the return statement are not executed (although the compiler warns you about this problem if you place statements after the return statement).

If you don’t want your method to return information (that is, its return type is void), you can use a variation of the return statement to cause an immediate exit from the method. You write the keyword return and follow it immediately by a semicolon. For example:

Click here to view code image

```
void showResult(int answer)
```