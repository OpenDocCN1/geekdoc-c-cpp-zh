```
```cpp
catch (double d)
{
    cout<<"Caught double\n";
}
    cout<<"end";
    return 0;
}
```
```

In the preceding program, the RestrictHandler() function can only throw the integer, character, and double exceptions. If it attempts to throw any other type of exception, then an abnormal program termination will occur.

Let's now learn how to catch an exception.

# ## Catching any Exception

The catch block is used to catch the exceptions in a program whenever such exceptions occurred within the program. This block generally follows the try block. We can specify the type of exception that we wish to catch in the catch block. This is determined by the exception declaration, which is mentioned within the set of parenthesis that follows the catch keyword.

The generic syntax of the catch block is as follows:

```
```cpp
try
{
    // Code ...
} catch (NameofException e)
{
    // code snippet that handles NameofException exception
}
```
```

If a function has zero exception specification, then any sort of exception can always be thrown. One solution to the present problem is to generate a handler that catches any sort of exception. This is done by using the ellipses in the argument list of catch(), shown as follows:

```
```cpp
catch(...)
{
    cout<<"An exception was thrown" << endl;
}
```
```

In the next section, let's learn how to re-throw an exception.

# ## Re-throwing an Exception

To re-throw an expression from within an exception handler, we can write a code block in such a way that we can call the throw statement with no exception in it. This will result in passing the current exception on to an outer try/catch sequence. Consider the following code:

```
```cpp
catch(...)
{
    cout<<"Let us throw this exception" << endl;
    throw;
}
```
```

Re-throwing an exception is mainly done to give multiple handlers access to the exception. We can only re-throw an exception from within a catch block or from any function called from within that block. In such cases, it will not be re-caught by the same catch statement; rather, it will propagate outward to the next catch statement. Consider the following example to illustrate the concept of re-throwing an exception: