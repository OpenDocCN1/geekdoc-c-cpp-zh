# Section 17.2.5 Termination Model
of Exception Handling

+   - C++ uses the **termination model of exception handling** (p. 763) in which control resumes with the first statement after the last `catch` handler following a `try` block
+   - A `try` block consists of keyword `try` followed by braces (`{}`) that define a block of code in which exceptions might occur. The `try` block encloses statements that might cause exceptions and statements that should not execute if exceptions occur.
+   - At least one `catch` handler must immediately follow a `try` block. Each `catch` handler specifies an exception parameter that represents the type of exception the `catch` handler can process.
+   - If an exception parameter includes an optional parameter name, the `catch` handler can use that parameter name to interact with a caught exception object.
+   - The point in the program at which an exception occurs is called the **throw point** (p. 763).
+   - If an exception occurs in a function and is not caught in that function, the function terminates immediately, and the program attempts to locate an enclosing `try` block in the calling function.