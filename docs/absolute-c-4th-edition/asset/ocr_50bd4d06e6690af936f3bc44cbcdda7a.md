# 18.2 **Programming Techniques for Exception Handling**

> *Only use this in exceptional circumstances.*
> 
> — Warren Peace, *The Lieutenant's Tool*

So far we have shown lots of code that explains how exception handling works in C++, but we have not shown an example of a program that makes good and realistic use of exception handling. However, now that you know the mechanics of exception handling, this section can go on to explain exception handling techniques.

# WHEN TO THROW AN EXCEPTION

We have given some very simple code to illustrate the basic concepts of exception handling. However, our examples were unrealistically simple. A more complicated but better guideline is to separate throwing an exception and catching the exception into separate functions. In most cases, you should include and throw statement within a function definition, list the exception in an exception specification for that function, and place the catch clause in a different function. Thus, the preferred use of the try–throw–catch triad is as illustrated here:

```
```cpp
void functionA() throw (MyException)
{
        .
        .
        .

        throw MyException(<Maybe an argument>);
        .
        .
        .
}
```
```

Then, in some other function (perhaps even some other function in some other file), you have the following:

```
```cpp
void functionB()
{
        .
        .
        .
}
```
```