![](bbox=[0.324, 0.089, 0.756, 0.265])

**Figure 14.7** A try-catch block with multiple catch clauses

# Hidden Throw Statement

Sometimes we see a *try-catch* block, but we cannot see the *throw* statement. This happens when we use a predefined or a library function whose definition we cannot see. We just see the function call in a *try* clause, but the function definition contains a *throw* statement. For example, some string member functions, such as the at() function, throws an exception if the index is out of range. When we call this function in our program, we may need to enclose the call in a *try-catch* block to catch the exception and prevent program abortion.

# Multiple Catch Clauses

Figure 14.7 shows a situation in which a function may throw two different types of exceptions. Since the handling for each type may be different, we can have two types of *catch* clauses.

# Generic Catch Clause

A *catch* clause may only catch exceptions of its parameter type. A *catch* clause of an integer type cannot catch an exception of a floating-point type when it is thrown. If we want to catch any type of exception, we can use an ellipsis as the parameter in the *catch* clause. In this case, if specific exception types need to be handled differently, the generic (any type) *catch* clause is coded as the last *catch* clause. The following shows such a *try-catch* block.

```
```text
try
{
    ...
}
catch (int x)  // Specific type catch
{
    ...
}
catch (...)  // Ellipsis means any exception type
{
    ...
}
```
```