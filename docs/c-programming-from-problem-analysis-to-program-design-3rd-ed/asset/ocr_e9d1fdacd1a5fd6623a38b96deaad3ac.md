called **catch clauses**. The code that you want executed regardless of whether an exception is thrown is placed in the `finally` block. The syntax for a `try...catch...finally` block is as follows:

```
```text
try
{
        // Statements
}
catch ([ExceptionClassName exceptionIdentifier])
{
        // Exception handler statements
}
:    // [additional catch clauses]
[finally]
{
        // Statements
}]
```
```

![](bbox=[0.173, 0.418, 0.236, 0.467])

The `:` is used in the examples in this book to indicate that additional statements may be added to the program listing. Here, the colon would have to be replaced by additional `catch` clauses.

More than one `catch` clause can be included. A `try` block must include at least one `catch` clause. Notice that a square bracket follows the keyword `catch` to indicate that the parentheses and the argument list are optional. Omitting the argument list makes the `catch` **generic**—meaning any exception that is thrown is handled by executing the code within that `catch` block. If you include an exception type as part of the argument list, only exceptions that match the type listed are handled by that `catch` clause. You will see examples using multiple `catch` clauses later in this chapter.

The `finally` clause is also optional. It can be included if there is a segment of code that needs to be executed, no matter what. If, for example, you have an open file or database connection, you can put the close statements in the `finally` block to make sure the file or connection is closed properly. When code is included in all three blocks for the `try...catch...finally` construct, the statements inside the `try` block are attempted first. If no problem exists and the `try` block code is finished, the `catch` clause(s) is (are) skipped, and control transfers into the `finally` block where that code is executed.

If an unexpected error occurs in the `try` block that throws an exception, the code in the `try` block is halted at the line that caused the problem. The CLR tries to find a matching exception handler within the current method. If one is found, control transfers to the first listed `catch` clause that can handle the type of exception thrown. The `catch` clause statements are executed, and control transfers to the `finally` block where its code is executed. Notice with both situations (exception thrown and no exception thrown) that if a `finally` block is included, the statements in it are executed.